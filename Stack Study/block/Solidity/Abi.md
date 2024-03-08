
> [!info]
> The Contract Application Binary Interface (ABI) is the standard way to interact with contracts in the Ethereum ecosystem, both from outside the blockchain and for contract-to-contract interaction. Data is encoded according to its type, as described in this specification. The encoding is not self describing and thus requires a schema in order to decode.

이더리움 환경안에서 스마트 컨트랙트를 상호작용시키는 표준방법 
# abi.encodeWithSignature
외부 함수를 사용 할 때  call 하거나 delegate call할경우에 
abi.encodeWithSignature(string memory signature, ...) returns (bytes memory)

# abi.encode vs abi.encodePacked

- abi.encode: ABI 표준에 따라, 각 인자는 32 바이트 단위로 패딩된다.
    - a = 0x12
    - b = 0x3456
    - 결과
        - 0x000000000000000000000000000000000000000000000000000000000000000120000000000000000000000000000000000000000000000000000000000003456
- abi.encodePacked(): 패딩 없이 연속적으로 인코딩된다.
    - a = 0x12
    - b = 0x3456
    - 결과
        - 0x123456

또한 공식문서에 따르면 abi.encodePacked를 서명에 사용하지말라고한다 그 이유는 다이니막한 타입이 있을 경우에 값이 다르게 나올수 있기 때문에 되도록이면 서명에는 
abi.encode 사용을 권장하였다 .. 

