# Call 
> low level 함수 

1. 송금하기 
2. 외부의 스마트 컨트랙트 함수 부르기
3. 가변적인 gas 
4. 이스탄불 하드포크 이후 gas 가격이 상승에 따라 call 사용권장
5.  re-entrancy(재진입) 공격 위험이 있기에, Checks_Effects_Interactions_Pattern 사용 

## 2번 외부의 스마트 컨트랙트 함수 부르기 
- 외부 스마트 컨트랙트의 함수를 사용하고 싶을 경우에 나의 caller의 컨트랙트 내부에는 함수의 기능없지만 외부 스마트 컨트랙트의 주소와 함수의 이름 인자등 시그니처를 알 수 있으면 호출이 가능하다 .

![[Pasted image 20240114194216.png]]

> msg.sender 에 주목
> 
# Delegate Call 
1. msg.sender 가 본래의 스마트 컨트랙트 사용자를 나타낸다.
2. delegate call이 정의된 스마트 컨트랙트 ( 즉 caller)가 외부 컨트랙트의 함수들을 마치 자신의 것 처럼 사용(실질적인 값도 caller에 저장된다)

>[!tip]  그래서 외부 컨트랙트와 caller 컨트랙트는 같은 변수를 가지고 있어야 한다.


> [!question] ### WHY? 
> upgradable smart contract 용도 



![[Pasted image 20240114194223.png]]

> msg.sender 에 주목 

```solidity
// SPDX-License-Identifier: MIT

pragma solidity >=0.8.0 <0.9.0;

  

contract add {

    event justFallback(string _str); // 정의되지 않는 함수를 호출 시도 할때

    event justReceive(string _str); // 이더 송금 받기 위해서

    uint256 public num = 0;

    event Info(address _addr,uint256 _num);

  

    function plusOne() public {

        num ++;

        emit Info(msg.sender,num);

    }

  

    function addNumber(uint256 _num1, uint256 _num2)

        public

        pure

        returns (uint256)

    {

        return _num1 + _num2;

    }

  

    fallback() external payable  {

        emit justFallback("Not Defined function");

        /*

            결국 fallback()함수는 존재하지 않거나 잘못된 방식으로 호출되었을 경우를 처리하기

            위함이기 때문에 revert같이 에러를 발생시켜 트랜잭션을 롤백시켜 컨트랙트안에 토큰이나 코인이 갇히는 걸 막는다

            revert문을 주석처리 후 실행할 경우 이더가 컨트랙트로 그냥 송금되어 사라지게된다.

        */

        revert("Roll Back");

  

    }

  

    receive() external payable {

        emit justReceive("Receive the coin");

    }

}

  

contract caller {

    uint256 public decodedData;

    uint256 public num = 0;

  

    event calledFunction(bool _success,bytes _output);

    event showDecodingValue(uint256);// decoding된 결과값 보여주기 위함

    //1. 이더 전송 {}괄호안에 조건 설정

    function transferEth(address payable _to) public payable {

        (bool success,) = _to.call{value: msg.value}(""); // 이더만 송금시는 bytes로 리턴값 받는게 없으니 공란으로 둔것

        require(success,"failed to tranfer ETH");

    }

    //2. 외부 함수 호출 이더를 전송하지 않기 때문에 {}입력 안한 것

    function callMethod(address _contractAddr,uint256 _num1,uint256 _num2) public {

        (bool success,bytes memory outputFromCalledFunction) = _contractAddr.call( // outputFrom~은 외부 함수를 호출해서 얻은 리턴값(bytes)

            abi.encodeWithSignature("addNumber(uint256,uint256)", _num1,_num2)

        );

  

        require(success,"Failed to call other contract's function");

        emit calledFunction(success, outputFromCalledFunction);// 32바이트 16진수로 나옴

        decodedData = abi.decode( outputFromCalledFunction, (uint256));

        emit showDecodingValue(decodedData);

    }

    // Fallback을 실행하기 위해서 존재하지 않는 함수 호출

    function callNotExistMethod(address _contractAddr) public payable {

        (bool success,bytes memory outputFromCalledFunction) = _contractAddr.call{value: msg.value}( // outputFrom~은 외부 함수를 호출해서 얻은 리턴값(bytes)

            abi.encodeWithSignature("NotExist()")

        );

  

        require(success,"Failed to call other contract's function");

        emit calledFunction(success, outputFromCalledFunction);

    }

  

    /*

        Call vs Delegate Call

        확실하게 외부함수를 가져다 끌어쓸 때는 delegate Call을 쓰는 게 좋다

        delegate call은 외부함수를 콜러함수에 옮겨 놓은 것 처럼 행동하기 때문에

        그렇게하면 caller 컨트랙트에는 state만 관리하게 두고 외부함수가 있는 컨트랙트를 수정이 필요할 경우

        기존에 call로 하게 되면 caller와 외부 컨트랙 전부 바꾸고 주소도 고객에게 다시 알려줘야되지만

        Delegate Call의 경우 새로운 로직이 들어간 외부 컨트랙(B2)을 배포하고 caller의 delegate Call의 주소를

        B2로 변경만 해주면 되기에 기존의 데이터는 caller에 저장되어 있어 데이터가 보전된다.

  

        caller 와 외부 함수의 변수는 같아야 된다.

  

        이것이 upgradable smart contract framework

  

     */

    function callNow(address _contractAddr) public payable {

        (bool success,) = _contractAddr.call(abi.encodeWithSignature("pluseOne()"));

        require(success,"failed to call");

    }

    function delegateCallNow(address _contractAddr) public payable {

        (bool success,) = _contractAddr.delegatecall(abi.encodeWithSignature("pluseOne()"));

        require(success,"failed to delegate call");

    }

}
```
