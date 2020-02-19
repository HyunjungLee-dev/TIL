## 추상 자료형

- 추상 자료형은 프로그램의 대상이 되는 사물이나 현상을 추상화하여 정의한 것.
- 사용자와 구현자의 분리
- 일반성(Generality)

[한빛미디어 추상 자료형 포스트](http://www.hanbit.co.kr/media/channel/view.html?cms_code=CMS9536454095&cate_cd=) / IT CookBook, C C++로 배우는 자료구조론



## 단순 연결 리스트(Single Linked List)

- 단순 연결 리스트의 ADT : ArrayList를 구현과 차이는 없고 정렬 기능만 추가

  - 초기화 / 삽입 / 조회 / 삭제 / 정렬

- 구현 사항을 결정해야하는 과정의 필요에 대한 질문

  Q. tail의 필요성은?

  Q. 첫 번째 Node 상황과 두 번째 Nod 상황이 나뉘지 않고 항상 같은 상황으로 만들 수 있을까?

**과제**

- LinkedRead.cpp -> Dummy Node 추가해보기
- ArrayList를 DLinkedList로 대처해서 구현해보기
- 함수포인터 / 콜백 코드 작성해보기
- 단순 연결 리스트 개념 공부



**참고 할 사이트**

- [소년코딩](https://boycoding.tistory.com/233 )
- https://norux.me/8



### Dummy Node _단순 연결 리스트(Single Linked List)

```c++
head = (Node*)malloc(sizeof(Node)); /*더미노드*/
tail = head;

/*** 노드의 추가과정 ***/
		newNode = (Node*)malloc(sizeof(Node));
		newNode->data = readData;
		newNode->next = NULL;
        /*
        if(head == NULL)
            head = newNode;
        else
            tail->next = newNode;
        */ //생략 되는 코드
		tail->next = newNode;

		tail = newNode;
```

더미 노드(Dummy Node)는 유효한 데이터를 지니지 않는 빈 노드를 의미하는데 이것을 넣는 이유는 첫 번째 노드와 두 번째 이후의 노드에 차이가 있는 것을 없애고 일관된 형태로 구성하기 위해서이다. 



### 단순 연결 리스트 정렬 삽입

```C++
typedef struct_linkedList
{
    Node* head;
    Node* cur;
    Node* before;
    int numOfData;
    int (*comp)(LData d1, LData d2);// 정렬의 기준을 등록하기 위한 멤버_함수포인터!
}LinkedList;
```

함수 포인터에 대한 이해가 필요하다.  LinkedList 구조체에 왜 함수 포인터가 있는가? 그건 정렬의 기준을 등록하기 위해서였다. 정렬을 할 때 오름차순만 있는 게 아니라 다양한 정렬 방식이 있다. 이 방식(기능)이 어떻게 바뀔지 예상할 수 없기에 거기에 대처하기 위해서 멤버에  함수 포인터가 존재하는 것이다. 필요한 기능을 가진 함수를 직접 만들어서 그 기준에 따라 반환된 값을 이용하여 정렬하면 되는 것이다.

**정렬 삽입을 구현하기 위해서**

- LinkedList의 정렬기준이 되는 함수를 등록하는 SetSortRule 함수
- SetSortRule 함수를 통해서 전달된 함수정보를 저장하기 위한 LinkedList의 멤버 comp
- Comp에 등록된 정렬기준을 근거로 데이터를 저장하는 SInsert 함수

**과제**

- 단순 연결 리스트 오름차순 / 내림차순 함수 작성해서 적용해보기.



## 원형 연결 리스트 (Circular linked list)

Last Node가 First Node를 가리키게 하는 리스트 . head 대신 tail만 존재하게 된다면 tail이 마지막 지점이면서 tail->next가 시작점이 된다. 또한 Node를 추가 할 때 두 가지 방법이 있는데 머리에 추가하느냐(tail->next 부분이 된다) 꼬리에 추가 하느냐 tail이 추가한 Node가 된다. (tail의 위치가 달리지는 것) // 블로그 참고 

[ Seongkyun Han's](https://seongkyun.github.io/data_structure/2019/03/20/data_structure/)

**과제**

- 원형 연결 리스트 예제 공부해보기	
  - 원형 연결 리스트 기반으로 프로그램 작성하기



## 양방향 연결 리스트(Double LinkedList )

이중 연결 리스트라고 부르기도 하며 왼쪽 Node가 오른쪽 Node를 가리킴과 동시에 오른쪽 Node도 왼쪽 Node를 가리키는 구조이다. 왼쪽과 오른쪽 모두 가리키고 있기 때문에 단순 연결리스트에서 참조를 위해 사용했던 before 은 필요가 없다.

삽입을 할 때 두 번째 이후에 Node를 추가할 때 head의 위치를 옮기는 것은 새롭게 추가한 Node를 기존의 head가 가리키는 Node와 연결한 후에 head를 옮겨주는 것이 옳다. 아니면 무엇을 가리켜야 할지 모르게 되게 때문이다.

양방향 연결 리스트에서 Node의 왼쪽으로 이동해서 해당 Node를 참조/삭제 할 수 있는데 이것이 뒤에 나오는 자료구조(스택/큐)를 이해하는데 도움이 될 것이다.

**과제**

<연결 리스트 만들어보기>

1. 양방향 연결 리스트
2. ## 더미 노드가 리스트의 앞과 뒤에 각각 존재
3. 포인터 변수 head와 tail이 있어 리스트의 앞과 뒤를 각각 가리킨다.



### Dummy Node_양방향 연결 리스트(Double LinkedList )

기존의 양방향 연결 리스트에서 더미노드 기반 연결 리스트를 구현할 때 코드를 추가/변경 해야하는 부분

**초기화**

더미 노드를 생성하고 head->prev / tail->next를 NULL로 초기화 시켜준다. 양방향 연결 리스트 이므로 head->next는 tail을 가르키게 되고 tail->prev는 head를 가리키게 된다.

**데이터 저장**

새 노드를 추가하는데 달라진 부분은 서로를 가리키게 해야한다는 것이다. 기존과 같이 새 노드를 생성하고 데이터를 저장한 다음 새 노드와 새 노드의 왼쪽에 위치할 노드가 서로를 가리키고 새 노드와  새 노드의 오른쪽에 위치할 노드가 서로를 가리키게 한다.

**조회**

tail이 존재하는만큼 현재 위치(cur  / 첫 조회의 경우는 head)의 다음이 tail인지 확인해야한다. tail일 경우는 더이상 찾을게 없다는 의미임으로 false를 반환한다.  아닌 경우는 현 위치를 다음으로 옮겨주며 데이터 값을 조회한다.

**삭제**

기존의 리스트들과 동일하게 삭제해야하는 노드를 알기 위해 노드를 하나 만들어 저장해준다 다음 삭제 하는 현 노드의 앞과 뒤에 있는 노드를 각각 연결해준다. 그 후 현재 위치를 삭제 하는 현 노드의 앞의 노드로 바꿔준다(앞인 이유는 뒤의 노드로 할 경우 조회시 현 노드는 조회했다고 여겨져 넘어가기 때문이다.) 모든 과정이 끝난후 저장했던 현 노드를 동적할당 해제(삭제)해준다.

여기서 코드를 작성할때, 노드 자체인지 아니면  next인지 prev인지 생각하자. 그림을 그려보는 것이 많은 도움이 된다! 



## 연결리스트의 장단점

### 장점

삽입이 간단하며 항목 생성 후 포인터 값만 변경해주면 된다.

### 단점

- 순차적으로 접근하므로 항목 접근이 오래 걸린다. (최대 O(n))
- 물리적으로 인접한 메모리에 위치해있지 않다.
- 참조 포인터를 위한 메모리 공간이 낭비 된다.