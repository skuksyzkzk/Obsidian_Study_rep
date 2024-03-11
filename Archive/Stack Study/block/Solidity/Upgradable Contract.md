# 구현에는 2가지 경우 존재

# 1. delegate call 사용하는 proxy


취약점이 발생하였을 경우에 그대로 이용해야 된다는 불편함이 존재 
하지만 delegate call을 통해서 upgradable 하게 작성이 가능하다 

블록체인의 불변성이라는 특성 때문에 한 번 저장된 데이터는 변경이나 삭제가 불가능하며 오로지 추가만 가능하다. 이는 스마트 컨트랙트를 작성할 때도 마찬가지다. 한 번 배포가 된 스마트 컨트랙트는 버그가 발견되더라도 변경이 불가능하다. 만약 수정된 새로운 컨트랙트를 배포하더라도 사용자에게 새로운 컨트랙트 주소를 전달해야 하며, 이전 데이터를 옮겨오는데 상당한 시간과 비용이 발생할 수 있다.


결국 Proxy Contract에 State 값을 다 저장시키고 그외의 로직은 외부 컨트랙트로 따로 분리해서 동작시키는 형태 


## implement랑 프록시 컨트랙트랑 실제 사용하는 state 값들이 순서대로 동일하게 작성이 되어야 한다.
안그러면 state colision이 생길수 있음 .

실행시에 어떻게 함수의 메소드의 인풋데이터인지 모른다 
![[Pasted image 20240114224932.png]]

저기 calldata에 들어갈부분이 바로 implev1의 함수 inc 데이타 근데 모른다 
그래서 inc를 실행시키고 input의 16진수 값을 복사해서 전송 

![[Pasted image 20240114225033.png]]

>input값이다 

![[Pasted image 20240114225135.png]]

그 다음 값을 붙여 넣은 다음에 트랜잭션을 실행하게 되면 x가 1로 저렇게 증가 되어있는 모습이다 


# 다른 로직을 사용하고 싶을 경우에는 다시 주소설정을 해주면 된다.


https://forum.openzeppelin.com/t/korean-writing-upgradeable-contracts/2007
https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/proxy
또한 openzepplin에도 proxy 사용 사례 가 있는데 
costructor를 사용하지 못하기에 initialize라는 것을 도입하였다 

들어가면 delegate call을 어셈블리로 표현한 것을 똑같이 확인 할수 있따

## 그리고 우리가 직접 proxy 컨트랙트를 구현해도 상관없지만 안전하게 openzepplin의 UUPS_poxy 컨트랙트를 수정해서 사용하는 것이 더 안전하다 .

# 2. interface 사용 

> defi 서비스에서 컨트랙트가 외부 토큰 컨트랙트를 호출 하는 경우가 존재하는데 그 때 많이 사용한다.

[[interface]]

