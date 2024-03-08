
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

print(type(lastestBlock))

dictLastesBlock = dict(lastestBlock)

print(type(dictLastesBlock))

print("###############")

print(json.dumps(dictLastesBlock,cls=HexJsonEncoder))

#print(Web3.to_json(lastestBlock))

#print(Web3.to_json(dictLastesBlock))

#print(Web3.to_json(lastestBlock)==Web3.to_json(dictLastesBlock))

print("###############")
```

이렇게 하였을 때 오류가 떠서 안되었다 
그래서 Web3.to_json을 하니 정상 작동하였다.