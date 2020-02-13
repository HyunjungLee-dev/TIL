<img src="https://img.shields.io/badge/Update-20.01.13-blue" align = "left">

#### 함수포인터(function pointer)

포인터는 다른 변수의 주소를 저장하는 변수이며 함수 포인터는 함수를 가리키는 변수. 즉, 함수의 주소를 저장하는 변수

```c++
typedef struct _linkedList
{
Node* head; 
Node* cur; 
Node* before; 
int numOfData; 
int (*comp)(LData d1, LData d2); // 정렬의 기준을 등록하기 위한 멤버_함수포인터!
}LinkedList
```

#### 콜백(callback)

다른 코드의 인수로서 넘겨주는 실행 가능한 코드



<img src="https://img.shields.io/badge/Update-20.01.14-blue" align = "left">

#### 함수 포인터  / 콜백 함수

함수의 주소를 저장했다가 해당 주소의 함수를 호출하는데 사용하는 포인터이며 자신이 사용할 함수의 원형을 자료형으로 사용한다. 아래 블로그 정독 할 것.

https://blog.naver.com/tipsware/221286052738
