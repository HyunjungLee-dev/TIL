## 스택(Stack) 

스택이란 후입선출(LIFO-Last In, First Out)방식의 자료 구조이다.  

### 자료구조의 ADT

```C
void StackInit(Stack* pstack);
//스택의 초기화

int SIsEmpty(Stack* pstack);
//스택이 빈 경우 TRUE, 그렇지 않은 경우 FALSE을 반환

void Spush(Stack* pstack, Data data);
// 스택에 데이터를 저장한다.

Data Spop(Stack* pstack);
// 마지막 저장된 요소를 삭제하고 삭제된 데이터는 반환 된다

Data Speek(stack* pstack);
// 마지막 데이터를 반환하되 삭제는 하지 않는다.
```

여기서  c로는 직접 함수를 만들어줘야하는데 위의 ADT 이름에 있는 push, pop, size, empty 로 만들어준 것은 **c++ STL**에서도 볼 수 있다. #include<stack>을 통해서 스택 라이브러리를 include 하여 사용 할 수 있다. 

c++ STL의 경우는 이 사이트를 참고 할 것

http://www.cplusplus.com/reference/stack/stack/stack/

스택의 경우 배열과 연결 리스트 기반으로 구현이 가능하다.  

### 배열 기반의 경우

데이터를 추가하고 꺼내 쓰고 하는 과정만 있어서 리스트 보다 상황이 다양하지 않으며 배열의 길이와 상관없이 인덱스 0이 항상 바닥에 위치한다. 마지막 데이터의 저장 위치를 기억해야한다.

```c
typedef struct _arrayStack
{
Data stackArr[STACK_LEN];
int topIndex;
}ArrayStack;
```

topIndex가 들어가게 된다.  마지막 데이터의 저장 위치를 저장하기 위함이고 초기화에서는 배열은 0부터이기 때문에 -1을 넣어 빈 상태를 만들어줘야한다.

### 연결 리스트 기반의 경우

저장된 정보가 역순으로 조회(삭제)가 가능한 연결 리스트이며 메모리 구조는 똑같은 모양을 하지만 ADT정의에서 함수의 역할이 다르다.

*연결 리스트에서는 저장된 순서를 유지하는 것은 필요 사항이 아니었기에 정렬 함수를 따로 만들었었고 양뱡향 연결리스트에서도 따로 함수를 만들어 Node의 왼쪽으로 이동해서 해당 Node를 참조/삭제 할 수 있었다. 스택의 경우는 자료를 관리한다는 것은 동일하지만 관리 방식(LIFO)이 미리 정해져 있다는 것이 다르다*

