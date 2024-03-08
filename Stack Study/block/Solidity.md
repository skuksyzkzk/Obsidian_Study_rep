
처음 만든 CSMM 테스트에서 

```
 describe("addLiquidity", async () => {

        //

        it("add liquidity", async () => {

          await token.approve(exchange.address, toWei(1000));

          await exchange.addLiquidity(toWei(1000), { value: toWei(1000) }); //이더리움하고 Gray토큰 1000개씩

          expect(await getBalance(exchange.address)).to.equal(toWei(1000));

          expect(await token.balanceOf(exchange.address)).to.equal(toWei(1000));

        });

      });
```

이 부분에서 addLiquidity 저 파트에서 value 부분

> `{ value: toWei(1000) }`: 이는 함수에 송금되는 Ether의 양을 지정하는 방법입니다. Ethereum의 스마트 계약에서 함수에 Ether를 전송하려면 해당 함수의 호출에 `{ value: amount }` 형태로 Ether를 첨부해야 합니다


## View ,Pure 

### **1.view :  storage state 를 읽을 수 있지만, 그 state 값을 변경할 수 없다.** **2.pure : storage state 를 읽으면 안되고, 그 state값을 변경할 수 도 없다.**


# Interface 

https://docs.soliditylang.org/en/v0.8.23/contracts.html#interfaces

공식 doc 

간단히 말하면, 인터페이스는 클래스가 구현해야 하는 메서드의 계약을 제공하며, 이러한 메서드는 암시적으로 가상 함수로 취급됩니다. 이러한 함수를 구현하는 클래스에서는 `override` 키워드를 명시적으로 사용하지 않아도 됩니다. 그러나 이러한 함수를 다시 오버라이드할 수 있으려면 원본 메서드가 명시적으로 `virtual`로 표시되어야 합니다.

## 사용하는 이유

1. **계약 간의 상호 작용:**
    
    - 인터페이스를 구현한 여러 계약은 인터페이스에서 정의한 메서드를 공유하게 됩니다. 이로써 서로 다른 계약들은 공통된 메서드를 호출하거나 이벤트를 발생시키는 등의 상호 작용을 할 수 있습니다.
2. **계약의 분리와 재사용성:**
    
    - 인터페이스를 사용하면 계약의 로직을 분리할 수 있습니다. 인터페이스는 특정 기능의 "계약 템플릿"처럼 작동하며, 다른 계약이 해당 인터페이스를 구현함으로써 템플릿의 기능을 사용할 수 있게 됩니다. 이는 코드의 재사용성을 높이고 계약 간의 의존성을 감소시킵니다.
3. **유연성과 확장성:**
    
    - 인터페이스를 사용하면 스마트 계약을 쉽게 확장하고 업그레이드할 수 있습니다. 새로운 기능이나 업그레이드가 필요한 경우, 새로운 계약을 작성하여 기존 인터페이스를 구현하면 됩니다. 이렇게 하면 새로운 기능을 추가하거나 계약을 업그레이드해도 기존의 상호 작용 코드를 수정하지 않아도 됩니다.

종합하면, 인터페이스는 솔리디티에서 계약 간의 상호 작용을 정의하고 표준화하기 위한 강력한 도구로 사용됩니다. 이를 통해 스마트 계약 생태계에서 표준을 정의하고 지켜내며, 유연성과 재사용성을 확보할 수 있습니다.

# msg.sender 

현재 스마트컨트랙트를 배포한 사람 


# Revert / require/assert 

### Assert 는 가스비를 환불안하고 다 소비하기에 테스트용으로만쓰자 

## Revert는 가스비도 환불해주고 특정한 조건문 없이 바로 에러메세지를 발생시킨다 .

# Overflow 

정수 오버플로우란 변수가 그 자료형의 최댓값을 초과하여 최솟값으로 되돌아가는 현상을 의미합니다. 예를 들어, uint8 자료형의 변수가 255에서 1을 더하면 0이 되는 것입니다. 이러한 상황이 컨트랙트 내에서 발생하면 예상치 못한 동작이 발생할 수 있습니다.


특히 토큰과 같은 자산을 다루는 스마트 컨트랙트에서는 오버플로우에 대한 방어적인 코드가 매우 중요합니다. 오버플로우가 발생하면 토큰의 총 공급량 등의 핵심 변수가 부정확해지며, 이는 심각한 보안 문제로 이어질 수 있습니다. 또한 사용자들이 예상하지 못한 토큰 잔액 변화 등으로 인해 손실을 입을 수 있습니다.

따라서 안전한 스마트 컨트랙트를 작성하기 위해서는 오버플로우 및 언더플로우와 같은 정수 오류에 대한 검사 및 방어가 필요합니다. 일반적으로는 SafeMath와 같은 라이브러리를 사용하여 산술 연산에서 오버플로우 및 언더플로우를 방지하는 방법을 채택합니다. SafeMath는 연산 전에 오버플로우 및 언더플로우를 확인하고, 문제가 있을 경우 트랜잭션을 중단시키는 역할을 합니다.

> [!warning]  ### 학교수업 시스템 프로그래밍에서 배웠던 것 처럼 overflow나 underflow는 보안상 해킹이나 공격으로 많이 사용되기에 중요하다..
## 그러나 0.8.0 이상부터는 overflow발생시 이전으로 트랜잭션을 되돌리게 자동으로 하게되었다. 
#### 근데 이렇게 트랜잭션을 되돌리면 당연히 그동안 과정에 사용된 가스비는 낭비되게 되어진다...

**unchecked 문법**은 솔리디티 버전 `0.8.0` 이상부터 사용할 수 있다.

내용인 즉슨, `0.8.0` 버전 이상부터는 대부분의 연산에 대하여 기본적으로 오버플로우와 언더플로우를 런타임 때 체크하게 되었다는 것이다. 만약 연산 결과가 위 두 문제 중에 하나를 발생시키면 트랜잭션 과정 중에 발생한 모든 것들을 되돌려버리고 이전 상태로 돌아가게 만든다.

기본 설정으로 대부분의 연산에 이런 검증 과정을 거치다보니, 당연히 혹은 거의 오버-언더플로우가 일어나지 않을 연산을 할 때도 불필요하게 사용된다. 이는 곧 가스비로 연결되게 된다. 그래서 충분히 보장되어있거나 굳이 필요하지 않을 경우에 검증과정을 생략하고 연산을 하기 위해 unchecked를 사용한다.


## 컨트랙트 생성 CREATE , CREATE2 

### Create2 를 컨트랙트 배포완료된 주소를 원하는 것으로 설정가능함 
## Create

([0xF0 OPCODE](https://ethervm.io/#F0))

**sender** 와 **nonce**를 이용하여 RLP 인코딩 후 생성하는 방식으로 nonce 증가함에 따라 생성되는 컨트랙트 주소가 변경 된다.

※ 컨트랙트에도 nonce 값은 존재하며 0이 아닌 1부터 시작한다 ([EIP-161](https://eips.ethereum.org/EIPS/eip-161))  
컨트랙트의 nonce 값은 컨트랙트가 다른 컨트랙트를 생성하는 경우에만 증가한다.

> keccak256(rlp([sender, nonce]))[12:]

## Create2

([EIP-1014](https://eips.ethereum.org/EIPS/eip-1014), [OxF5 OPCODE](https://ethervm.io/#F5))

**0xff, address, salt, initcode** 를 통해 컨트랙트를 생성하는 방식으로, 같은 값을 사용한다면 동일한 주소로 컨트랙트를 생성 할 수 있다. (일반적으로 동일 주소로 재배포는 불가능하며 selfdesturct를 통해 삭제했을 경우 가능)

> keccak256( 0xff ++ address ++ salt ++ keccak256(init_code))[12:]

  
Create2 사용에는 Solidity 0.6.0 버전 이전과 이후로 나뉘어진다.  
  

**Solidity 0.6.0 버전 이전**

**new** 키워드를 사용하여 컨트랙트를 생성할 때 **salt** 값을 직접 사용하는 것이 불가능해서 **creat2** 함수를 사용하여 컨트랙트를 생성하는 방법을 사용하였다.

```javascript
UniswapV2Factory.sol

   bytes memory bytecode = type(UniswapV2Pair).creationCode;
   bytes32 salt = keccak256(abi.encodePacked(token0, token1));
   assembly {
       pair := create2(0, add(bytecode, 32), mload(bytecode), salt)
   }
```

※ creationCode는 컨트랙트 생성 바이트코드를 나타낸다, assembly 코드를 이용할때 creationCode 이용하여 컨트랙트 생성

  

**Solidity 0.6.0 버전 이후**

**new** 키워드에서 **salt** 값을 사용하여 컨트랙트를 생성하는 기능이 추가되어, 이를 통해 create2 함수를 사용하지 않고도 예측 가능한 주소에 컨트랙트를 생성할 수 있게 됬었다.

```javascript
contract D {
    uint public x;
    constructor(uint a) {
        x = a;
    }
}

contract C {
    function createDSalted(bytes32 salt, uint arg) public {
        // This complicated expression just tells you how the address
        // can be pre-computed. It is just there for illustration.
        // You actually only need ``new D{salt: salt}(arg)``.
        address predictedAddress = address(uint160(uint(keccak256(abi.encodePacked(
            bytes1(0xff),
            address(this),
            salt,
            keccak256(abi.encodePacked(
                type(D).creationCode,
                abi.encode(arg)
            ))
        )))));

        D d = new D{salt: salt}(arg);
        require(address(d) == predictedAddress);
    }
}
```