[[Plan]]

[[UniSwap V3 코드 분석]]

# 목표 

>VictionPay: an SDK that allows users to pay with $VIC or any TRC25 tokens.

### 구상

어떻게 해야 구현이 되어야 할까? 

> [!note ] 스왑 기능의 필요성과 VIC 나 TRC25 토큰을 화폐로 하는 Payment
> #### 스왑 기능은 사실 핵심은 아님 핵심은 결국 VIC or TRC25 토큰을 Payment 즉 결제의 수단으로 사용해야 하는 것
> ##### 그렇다면 스왑은 왜?? 
> 여기서 또 다른 선택지가 생겨나는 것 Viction의 화폐로 결제가 안되는(받지 않는)회사의 존재



## VIC or TRC25 토큰을 단순하게 상대방의 계좌로 보낸다 

- 여기서 상대방의 계좌가 E-market의 게좌이면 그 회사로 결제가 된 것이기에 단순하게 보았을 때 결국 결제 수단(화페)로서 사용을 한 것이다.

> [!tood] 계좌로 보내는 방법은 viction 홈페이지나  GPT 등 여러 수단으로 활용해서 실제로 가능한지 Testnet(viction testnet : ChainId 89) 에서 직접 확인해야된다.
> 



