
https://docs.openzeppelin.com/contracts/5.x/access-control#ownership-and-ownable
https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable

# ownership에 관련된 컨트랙트
초기에 컨트랙트를 배포할때 owner 주소를 선언한다 같이 
그럼으로써 onlyowner 모디파이어도 제공받는다
편하게 사용할 수 있다
onlyOwner만 사용가능한 함수에서 쓰기 좋고 내가 직접 구현 안해도 되서 
그리고 ownership을 renounce로 아예 없애버릴수도 있다
근데 그러면 onlyOwner로 되어있는 함수에 접근이 불가능하다
또한 컨트랙트의 owner를 변경도 가능하게 해준다 
```jsx 
// SPDX-License-Identifier: MIT

// OpenZeppelin Contracts (last updated v5.0.0) (access/Ownable.sol)

  

pragma solidity ^0.8.20;

  

import {Context} from "../utils/Context.sol";

  

/**

 * @dev Contract module which provides a basic access control mechanism, where

 * there is an account (an owner) that can be granted exclusive access to

 * specific functions.

 *

 * The initial owner is set to the address provided by the deployer. This can

 * later be changed with {transferOwnership}.

 *

 * This module is used through inheritance. It will make available the modifier

 * `onlyOwner`, which can be applied to your functions to restrict their use to

 * the owner.

 */

abstract contract Ownable is Context {

    address private _owner;

  

    /**

     * @dev The caller account is not authorized to perform an operation.

     */

    error OwnableUnauthorizedAccount(address account);

  

    /**

     * @dev The owner is not a valid owner account. (eg. `address(0)`)

     */

    error OwnableInvalidOwner(address owner);

  

    event OwnershipTransferred(address indexed previousOwner, address indexed newOwner);

  

    /**

     * @dev Initializes the contract setting the address provided by the deployer as the initial owner.

     */

    constructor(address initialOwner) {

        if (initialOwner == address(0)) {

            revert OwnableInvalidOwner(address(0));

        }

        _transferOwnership(initialOwner);

    }

  

    /**

     * @dev Throws if called by any account other than the owner.

     */

    modifier onlyOwner() {

        _checkOwner();

        _;

    }

  

    /**

     * @dev Returns the address of the current owner.

     */

    function owner() public view virtual returns (address) {

        return _owner;

    }

  

    /**

     * @dev Throws if the sender is not the owner.

     */

    function _checkOwner() internal view virtual {

        if (owner() != _msgSender()) {

            revert OwnableUnauthorizedAccount(_msgSender());

        }

    }

  

    /**

     * @dev Leaves the contract without owner. It will not be possible to call

     * `onlyOwner` functions. Can only be called by the current owner.

     * 

     * NOTE: Renouncing ownership will leave the contract without an owner,

     * thereby disabling any functionality that is only available to the owner.

     */

    function renounceOwnership() public virtual onlyOwner {

        _transferOwnership(address(0));

    }

  

    /**

     * @dev Transfers ownership of the contract to a new account (`newOwner`).

     * Can only be called by the current owner.

     */

    function transferOwnership(address newOwner) public virtual onlyOwner {

        if (newOwner == address(0)) {

            revert OwnableInvalidOwner(address(0));

        }

        _transferOwnership(newOwner);

    }

  

    /**

     * @dev Transfers ownership of the contract to a new account (`newOwner`).

     * Internal function without access restriction.

     */

    function _transferOwnership(address newOwner) internal virtual {

        address oldOwner = _owner;

        _owner = newOwner;

        emit OwnershipTransferred(oldOwner, newOwner);

    }

}
```