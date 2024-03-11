https://docs.soliditylang.org/en/v0.8.23/contracts.html#using-for

# using A for B 

## A 
1. 함수이름,함수리스트들 
2. non private function, library 이름  
A로 전달되야 하는 파라메터는 다음과 같다 

## B
1. 적용하고자 하는 type 
적용하고자 하는 type을 입력한다.*는 모든 타입에 적용시킴을 의미한다

> [!example]
> using SafeMath for uint8 
> uint8에 SafeMath 라이브러리에 있는 모든 함수를 적용시킨다는 뜻 



The directive `using A for B` can be used to attach functions (`A`) as operators to user-defined value types or as member functions to any type (`B`). The member functions receive the object they are called on as their first parameter (like the `self` variable in Python). The operator functions receive operands as parameters.

It is valid either at file level or inside a contract, at contract level.

The first part, `A`, can be one of:

- A list of functions, optionally with an operator name assigned (e.g. `using {f, g as +, h, L.t} for uint`). If no operator is specified, the function can be either a library function or a free function and is attached to the type as a member function. Otherwise it must be a free function and it becomes the definition of that operator on the type.
    
- The name of a library (e.g. `using L for uint`) - all non-private functions of the library are attached to the type as member functions
    

At file level, the second part, `B`, has to be an explicit type (without data location specifier). Inside contracts, you can also use `*` in place of the type (e.g. `using L for *;`), which has the effect that all functions of the library `L` are attached to _all_ types.


