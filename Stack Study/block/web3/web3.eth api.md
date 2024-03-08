
web3.eth 에서 get으로 받아오는 것들은 대부분 리턴값이 
attirbutedict라서 dict로 변환을 해줘야된다 아니면 
to_json을 쓰던지 

# Eth.get_transaction(_transaction_hash_)[](https://web3py.readthedocs.io/en/stable/web3.eth.html#web3.eth.Eth.get_transaction "Permalink to this definition")

- Delegates to `eth_getTransactionByHash` RPC Method
    

Returns the transaction specified by `transaction_hash`. If the transaction cannot be found throws `web3.exceptions.TransactionNotFound`.

```python
txList = lastestBlock.transactions

for tx in txList:

    print("###############")

    print(Web3.to_hex(tx))

    txDetail = w3.eth.get_transaction(Web3.to_hex(tx))

    print(json.dumps(dict(txDetail),cls=HexJsonEncoder))

    print("###############")
```

> 여기서 찍어보면 트랜잭션의 rvs 서명정보도 나오고 여러가지 해시정보 인풋데이터등이 출력된다.

