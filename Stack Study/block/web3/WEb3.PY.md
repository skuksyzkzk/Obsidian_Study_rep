
web3가 결국 나온 이유는 백엔드와 프론트엔드 연동 돕기 위해서 나온 것 이다
실제로 이더리움 노드에 접근해서 트랜잭션을 조회하거나 데이터를 조회 해보자

원래 rinkeby는 poa로 작동하는 것이라 middelware에서 poa를 임포트해줘야하지만 
sepolia는 pos로 작동하기에 임포트하지 않아도 된다.

>web3.py는 결국 web3.js에서 파생된것 

**web3.py** is a Python library for interacting with Ethereum.

It’s commonly found in [decentralized apps (dapps)](https://ethereum.org/dapps/) to help with sending transactions, interacting with smart contracts, reading block data, and a variety of other use cases.

# 데이터 조회 

```python
#https://sepolia.infura.io/v3/dd0193022d23482d803562851cdd175d

from web3 import Web3

import json # 추후 데이터를 편하게 보기 위함

  

from hexbytes import HexBytes

  

class HexJsonEncoder(json.JSONEncoder):

    def default(self,obj):

        if isinstance(obj,HexBytes):

            return obj.hex()

        return super().default(obj)

w3 = Web3(Web3.HTTPProvider('https://sepolia.infura.io/v3/dd0193022d23482d803562851cdd175d'))

  

print("###############")

print(w3.is_connected())# 연결확인

print("###############")

  

print("Get Last Block")

lastestBlock = w3.eth.get_block('latest')#블록에서 조회한 형태가 json형태로 날라오기 때문에 변환 시켜줘야된다.

print("###############")

# print(json.dumps(dictLastesBlock,cls=HexJsonEncoder))

print(Web3.to_json(lastestBlock))

print("###############")

  

# 블록의 실제 트랜잭션 데이터들을 조회한다.

print("start")

txList = lastestBlock.transactions

for tx in txList:

    print("###############")

    txDetail = w3.eth.get_transaction(Web3.to_hex(tx))

    print(json.dumps(dict(txDetail),cls=HexJsonEncoder))

    print("###############")
```

# 트랜잭션 전송

> 계정정보가 필요하다 메타마스크 비공개 키를 내보낸다음 private key가 필요 이걸로 트랜잭션을 생성 

```python
from web3 import Web3

import json # 추후 데이터를 편하게 보기 위함

from eth_account import Account

  

w3 = Web3(Web3.HTTPProvider('https://sepolia.infura.io/v3/dd0193022d23482d803562851cdd175d'))

  

PRIVATE_KEY = '5e0c2bef0801c73311c7d6428c15bc062ad2a4f13c4771b5cfd8a69df4cc7ea0'

print("private key : ",PRIVATE_KEY)

account = Account.from_key(PRIVATE_KEY)

print("Account address: ",account.address)

print("Account Balance: ",w3.eth.get_balance(account.address))
```

이렇게 하면 잔액정보도 확인이 가능하다

## 이더리움 전송하기 
### Eth.sign_transaction(_transaction_)[](https://web3py.readthedocs.io/en/stable/web3.eth.html#web3.eth.Eth.sign_transaction "Permalink to this definition")

- Delegates to `eth_signTransaction` RPC Method.
    

Returns a transaction that’s been signed by the node’s private key, but not yet submitted. The signed tx can be submitted with `Eth.send_raw_transaction`

트랜잭션이 완전한 형태로 나옴 
이거를 통해서 사인한 트랜잭션을 send raw transaction으로 전송한다 

### Eth.send_raw_transaction(_raw_transaction_)[](https://web3py.readthedocs.io/en/stable/web3.eth.html#web3.eth.Eth.send_raw_transaction "Permalink to this definition")

- Delegates to `eth_sendRawTransaction` RPC Method
    

Sends a signed and serialized transaction. Returns the transaction hash as a HexBytes object.

### Web3.to_wei(_value_, _currency_)[](https://web3py.readthedocs.io/en/stable/web3.main.html#web3.Web3.to_wei "Permalink to this definition")

Returns the value in the denomination specified by the `currency` argument converted to wei.

> Web3.to_wei(1, 'ether')
1000000000000000000


### Eth.wait_for_transaction_receipt(_transaction_hash_, _timeout=120_, _poll_latency=0.1_)[](https://web3py.readthedocs.io/en/stable/web3.eth.html#web3.eth.Eth.wait_for_transaction_receipt "Permalink to this definition")

Waits for the transaction specified by `transaction_hash` to be included in a block, then returns its transaction receipt.

Optionally, specify a `timeout` in seconds. If timeout elapses before the transaction is added to a block, then [`wait_for_transaction_receipt()`](https://web3py.readthedocs.io/en/stable/web3.eth.html#web3.eth.Eth.wait_for_transaction_receipt "web3.eth.Eth.wait_for_transaction_receipt") raises a `web3.exceptions.TimeExhausted` exception.

```python
from web3 import Web3

import json # 추후 데이터를 편하게 보기 위함

from eth_account import Account

  

w3 = Web3(Web3.HTTPProvider('https://sepolia.infura.io/v3/dd0193022d23482d803562851cdd175d'))

  

PRIVATE_KEY = '5e0c2bef0801c73311c7d6428c15bc062ad2a4f13c4771b5cfd8a69df4cc7ea0'

print("private key : ",PRIVATE_KEY)

account = Account.from_key(PRIVATE_KEY)

print("Account address: ",account.address)

print("Account Balance: ",w3.eth.get_balance(account.address))

  

print("#######################################################")

  

signedTransaction = w3.eth.account.sign_transaction(dict(

    nonce = w3.eth.get_transaction_count(account.address)# 논스 먼저 설정한는 이유는 기존의 논스를 몇 번 사용했는지를 확인해야지만 이중지불공격이 발생안함

    ,gas=30000

    ,maxFeePerGas= 3000000000

    ,maxPriorityFeePerGas = 3000000000

    ,to='0x4D225656f2B1c262e1C61a85b4c7DD85aCEfD217'

    ,value=w3.to_wei(0.001,'ether')

    ,data=b'first Transaction From Web3py'

    ,chainId=11155111

    ,

),PRIVATE_KEY)

print(signedTransaction)

print("#######################################################")

  
  

print("start")

w3.eth.send_raw_transaction(signedTransaction.rawTransaction)

# 실제로 잘 보내졌는지 확인하기 위해서 ether scan을 가지 않아도 서버에서 확인이 가능하다

print("pass")

print(w3.eth.wait_for_transaction_receipt(signedTransaction.hash))

print("finish")
```

nonce 값이 already know나 replacement 에러가 발생했을경우에는 
get_transactino_count(address,'pending')+1 을 해서 새롭게 트랜잭션을 날릴수있다.


# ERC20 토큰을 배포한뒤 그 정보를 가지고 네트워크에 트랜잭션들을 전송을 해보자 

컨트랙트 함수를 call할때는 
contract.functions.함수이름().call() 해주면 된다 
```python
from web3 import Web3

import json # 추후 데이터를 편하게 보기 위함

from eth_account import Account

  

w3 = Web3(Web3.HTTPProvider('https://sepolia.infura.io/v3/dd0193022d23482d803562851cdd175d'))

  

PRIVATE_KEY = '5e0c2bef0801c73311c7d6428c15bc062ad2a4f13c4771b5cfd8a69df4cc7ea0'

print("private key : ",PRIVATE_KEY)

account = Account.from_key(PRIVATE_KEY)

print("Account address: ",account.address)

print("Account Balance: ",w3.eth.get_balance(account.address))

  

contractAddr = "0xAdBA7DC2600c6fFBB5dDB4f85D33CeC3147Fc404"

with open('./ERC20.json') as f:

    abi = json.load(f) # 파일의 모든 데이터를 json형태로 가져온다.

  

fctokenCa = w3.eth.contract(address=contractAddr,abi=abi)# 인스턴스를 생성해서 이 인스턴스로 트랜잭션이나 날리는게 가능하다

  

print("########################################")

print("Contract Address: ",contractAddr)

print("Symbol: ",fctokenCa.functions.symbol().call())

print("Owner balance: ",fctokenCa.functions.balanceOf(account.address).call())

print("########################################")
```

# 다른 사용자에게 토큰 전송 : 트랜잭션 사용 

state를 바꾸는 트랜잭션을 할경우에는 transact()를 하면 된다.



