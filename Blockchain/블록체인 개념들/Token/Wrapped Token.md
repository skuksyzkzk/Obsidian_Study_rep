
"Wrapped token"은 주로 다른 블록체인 자산을 Ethereum 블록체인으로 가져오기 위해 사용되는 토큰을 나타냅니다. 이는 특정 자산을 다른 형태의 토큰으로 "래핑"하는 과정을 의미합니다. 대표적인 예로는 "Wrapped Bitcoin (WBTC)"이 있습니다.

Wrapped Bitcoin (WBTC)의 경우, Bitcoin을 Ethereum 블록체인에 가져오기 위해 사용됩니다.

• ERC20 표준은 ETH 보다 나중에 나온 표준이고 ETH와 ERC20은 구현이 다르다. 
• ETH는 이더리움의 프로토콜 레벨에서 구현이 된 것이기 때문에 SmartContract로 컨트롤 하는 것에 한계가 있다. ETH 전송 정도는 가능하지만 ERC20에서 보았던 approve, allowance 같은 함수는 사용 할 수 없다. • 디파이 서비스의 구현과 동작을 더 간단하게 하기 위해서 이더리움을 사용하지 않고 이더리움을 ERC20 형태로 만든 토큰을 사용한다

## 결국 ETH를 WETH로 래핑하는 이유는 ETH는 스마트컨트랙트 사용이 안되기에 ERC 20 토큰화 시켜서 Defi 서비스에서 호환성을 맞추고 사용하기 위함 
