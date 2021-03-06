## 우선순위 큐(Priority Queue)와 힙(Heap)

우선 순위 큐라는 것은 단순 큐의 확장 개념이 아니다. 큐의 경우 먼저 들어간게 먼저 나오는 FIFO(First In First Out)구조로 저장하는 형식이었다. 우선 순위 큐의 경우에는 각 원소들이 우선순위를 갖고 있으며 들어간 순서와 상관 없이 우선순위가 높은 데이터가 먼저 나오게 된다.  만약 두 원소가 같은 우선순위를 가진다면 큐에서 그들의 순서에 의해 처리된다.

우선순위 큐의 구현 방법으로는 큐나 스택처럼 배열과 연결리스트 기반으로 구현하는 것을 생각할 수 있는데 데이터 우선순위로 정렬을 해서 앞쪽부터 위치시켜 구현이 가능하지만 **단점**이 존재한다.

 **배열의 경우**는 데이터 삽입 및 삭제 과정에서 한 칸씩 밀거나 당기는 연산을 수반해야하며 삽입 위치를 찾기 위해서 모든 데이터와 비교 해야 한다.

**연결리스트의 경우**는 삽입의 위치를 찾기 위해 첫번째 노드에서 시작해 마지막 노드까지 저장된 데이터와 우선순위를 비교 진행해야한다. 

배열과 연결리스트에는 구현이 쉬운 대신 이러한 단점이 있기에 우선순위 큐를 구현하는 방법으로 **힙(Heap)**을 이용하는 것이 일반적이다.

- 힙은 완전 이진 트리이다.
- 모든 노드에 저장된 우선 순위의 조건이 자식 노드의 조건보다 루트 노드의 조건이 우선시 되어야 한다.
- 자식 노드 데이터의 우선순위 <= 부모 노드 데이터의 우선순위

힙을 구현하기 앞서 힙은 크게 두 가지가 있는데 최대 힙과 최소 힙이다.

- 최대 힙 : 루트 노드로 올라갈 수록 저장된 값(우선순위가 될 수도 있는)이 커지는 완전 이진 트리
- 최소 힙 :  루트 노드로 올라갈 수록 저장된 값(우선순위가 될 수도 있는)이 작아지는 완전 이진 트리

배열, 연결 리스트, 힙의 시간 복잡도 비교

- 배열과 연결리스트 데이터 삽입의 시간 복잡도는  O(n)
- 배열과 연결리스트 데이터 삭제의 시간 복잡도는 O(1)
- 힙은 데이터 삽입과 삭제 모두 시간 복잡도가 O(log₂n)

**힙의 구현**은 연결리스트로 힙을 구현 할 경우 마지막 위치를 특정하기 어렵기 때문에 힙은 노드에 우선순위를 추가해줘야하는 부분이 배열 인덱스로 활용하면 되기 때문에 배열을 기반으로 구현한다.

> **참고** 
>
> [wiki](https://ko.wikipedia.org/wiki/우선순위_큐)
>
> [seongkyun blog](https://seongkyun.github.io/data_structure/2019/08/07/data_structure/)
>
> 학원 PPT 자료

**과제**

SimpleHeap 코드를 보면서 분석 하며 이해해보기.



### 힙(Heap)의 개선

SimpleHeap.h 구조체

```c
typedef char HData;
typedef int Priority;

typedef struct _heapElem
{
	Priority pr;	// 값이 작을수록 높은 우선순위
	HData data;
} HeapElem;

typedef struct _heap
{
	int numOfData;
	HeapElem heapArr[HEAP_LEN];
} Heap
```

SimpleHeap.c / Insert 함수

```c
void HInsert(Heap * ph, HData data, Priority pr)
{
	int idx = ph->numOfData + 1;
	HeapElem nelem = { pr, data };

	while (idx != 1)
	{
		if (pr < (ph->heapArr[GetParentIDX(idx)].pr))
		{
			ph->heapArr[idx] = ph->heapArr[GetParentIDX(idx)];
			idx = GetParentIDX(idx);
		}
		else
			break;
	}

	ph->heapArr[idx] = nelem;
	ph->numOfData += 1;
}
```

기존의 SimpleHeap의 구조체와 데이터를 저장하는 HInsert 함수를 보았을때 단점이 있는데 단점은 사용자가 직접 데이터의 우선순위를 결정해야한다는 점이다. 따라서 일관성을 위하여 입력된 data를 기반으로 프로그램이 알아서 우선순위를 결정하는 것이 합리적이다. 그렇게 바꾸기 위해서는 구조체를 변경하면 된다.

UsefulHeap.h 구조체

```c
typedef char HData;

// d1의 우선순위가 높다면 0보다 큰 값
// d2의 우선순위가 높다면 0보다 작은 값
// d1과 d2의 우선순위가 같다면 0을 반환
typedef int PriorityComp(HData d1, HData d2);

typedef struct _heap
{
	PriorityComp * comp;
	int numOfData;
	HData heapArr[HEAP_LEN];
} Heap;
```

데이터에  근거하여 자동으로 우선순위를 결정하고자 한다면 함수를 멤버로 선언한 구조체를 만들면 된다. SimpleHeap과 달라진점은 HeapElem를 받아 구조체가 완성 되었다고 하면  UsefulHeap의 경우는 * comp 라는 함수를 멤버로 선언하여 멤버에 우선순위를 결정하는 함수의 주소값을 저장하게 된다. 이 함수에 의해 데이터에 따라 우선순위가 반환 될 것이다.

```c
int DataPriorityComp(char ch1, char ch2)
{
	return ch2 - ch1; // 아스키코드 이용
	//	return ch1-ch2;
}
```

PriorityComp형 함수의 경우에는  우선순위의 기준은 사용자의 편의에 따라 바꿔 만들 수 있다.

```c
void HeapInit(Heap * ph)
{
	ph->numOfData = 0;
} // SimpleHeap Init 함수

void HeapInit(Heap * ph, PriorityComp pc)
{
	ph->numOfData = 0;
	ph->comp = pc;// 우선순위 결정하는 함수의 등록
} // UsefulHeap Init 함수

void HInsert(Heap * ph, HData data, Priority pr) // SimpleHeap
void HInsert(Heap * ph, HData data) //UsefulHeap 

```

함수 포인터를 멤버로 선언했을때 Init 함수와 Inset 함수도 변하게 된다.  Insert의 경우  pr을 인자로 받지 않고 구조체 내의 comp 함수와 data 로 우선순위가 설정된다. 

UsefulHeap.c 의 GetHiPriChildDX 함수

```c
int GetHiPriChildIDX(Heap * ph, int idx)
{
	if (GetLChildIDX(idx) > ph->numOfData) // 자식 노드가 없다면
		return 0;

	else if (GetLChildIDX(idx) == ph->numOfData) // 왼쪽 자식 노드가 마지막 노드라면
		return GetLChildIDX(idx);

	else // 자식 노드가 둘 다 존재하므로 왼쪽 자식 노드와 오른쪽 자식 노드의 우선순위 비교
	{
		//	if(ph->heapArr[GetLChildIDX(idx)].pr 
		//				> ph->heapArr[GetRChildIDX(idx)].pr)
		if (ph->comp(ph->heapArr[GetLChildIDX(idx)],
			ph->heapArr[GetRChildIDX(idx)]) < 0)
			return GetRChildIDX(idx);
		else
			return GetLChildIDX(idx);
	}
}
```

GetHiPriChildDX 함수는 Delete를 도와주는 핵심 함수였다. 함수의 기능은 노드의 인덱스 값을 전달하면, 이 노드의 두 자식 중 우선순위가 높은 것의 인덱스 값을 반환하는 것이었다. Delete를 하게 될경우 가장 우선순위가 높은 루트 노드부터 삭제가 되는데 우선순위를 확인해 삭제가 된 루트 노드에 루트 노드의 우선 순위가 높은 자식 노드가 들어가야하기 때문이다.

하나씩 나누어 보도록 하자.

```c
if (GetLChildIDX(idx) > ph->numOfData) // 자식 노드가 없다면
		return 0;
```

GetLChildIDX(idx)는 왼쪽 자식 노드의 인덱스 값을 반환 하는 함수이다. 이 함수가 반환 하는 값이 numOfData 보다 클 경우 자식 노드가 없는 이유는 힙은 완전 이진 트리이다. 완전 이진 트리는 왼쪽부터 차례대로 삽입하는 트리이다.  numOfData는 마지막 노드의  값보다 왼쪽 자식의 인덱스 값을 반환하는 GetLChildIDX(idx)이 크다면 자식 노드가 없는 것이 된다.

```c
else if (GetLChildIDX(idx) == ph->numOfData) // 왼쪽 자식 노드가 마지막 노드라면
		return GetLChildIDX(idx);
```

위의 내용과 같은 생각을 해볼 수 있다. 힙은 왼쪽부터 차례때로 삽입 되는 완전 이진 트리이기 때문에 왼쪽 자식 노드의 인덱스 값이 마지막 노드의 값과 같으면 그 왼쪽 자식 노드가 마지막이라는 것과 같은 의미이며 오른쪽까지 확인해볼 필요는 없다.

```c
else // 자식 노드가 둘 다 존재하므로 왼쪽 자식 노드와 오른쪽 자식 노드의 우선순위 비교
	{
		//	if(ph->heapArr[GetLChildIDX(idx)].pr 
		//				> ph->heapArr[GetRChildIDX(idx)].pr)
       //SimpleHeap의 내용
		if (ph->comp(ph->heapArr[GetLChildIDX(idx)],
			ph->heapArr[GetRChildIDX(idx)]) < 0)
			return GetRChildIDX(idx);
		else
			return GetLChildIDX(idx);
	}
```

기존의 SimpleHeap 에서는 pr을 직접 비교했지만 comp 를 통해 데이터를 직접 넘겨 우선순위를 확인할 수 있다.

UsefulHeap의 HInsert 함수

```c
void HInsert(Heap * ph, HData data)
{
	int idx = ph->numOfData + 1;

	while (idx != 1)
	{
		//	if(pr < (ph->heapArr[GetParentIDX(idx)].pr))
		if (ph->comp(data, ph->heapArr[GetParentIDX(idx)]) > 0)
		{
			ph->heapArr[idx] = ph->heapArr[GetParentIDX(idx)];
			idx = GetParentIDX(idx);
		}
		else
		{
			break;
		}
	}

	ph->heapArr[idx] = data;
	ph->numOfData += 1;
}
```

UsefulHeap의  HDelete 함수

```c
HData HDelete(Heap * ph)
{
	HData retData = ph->heapArr[1];
	HData lastElem = ph->heapArr[ph->numOfData];

	int parentIdx = 1;
	int childIdx;

	while (childIdx = GetHiPriChildIDX(ph, parentIdx))
	{
		//	if(lastElem.pr <= ph->heapArr[childIdx].pr)
		if (ph->comp(lastElem, ph->heapArr[childIdx]) >= 0)
			break;

		ph->heapArr[parentIdx] = ph->heapArr[childIdx];
		parentIdx = childIdx;
	}

	ph->heapArr[parentIdx] = lastElem;
	ph->numOfData -= 1;
	return retData;
}
```

HInsert와 HDelete 의 함수도 살펴보면 comp에 등록된 함수의 호출결과를 통해서 우선순위를 판단하는 것을 볼 수 있다.



### 우선순위 큐 자료구조의 ADT

앞서 우선순위 큐를 구현할때 힙을 이용하는 것이 일반적이라고 했다. 그렇게면 우선순위 큐 자료구조의 ADT를 먼저 생각해보자. 당연히 Init 초기화 하는 함수가 필요할 것이고 비어있는지 확인하는 Empty, 큐에서와 같이 enqueue, dequeue 가 필요할 것이다. 그렇게 작성된 ADT는 아래와 같다.

- void PQueueInit(Peueue* ppq, PriorityComp pc);
  - 우선순위 큐의 초기화를 진행
  - 우선순위 큐 생성 후 제일 먼저 호출되어야 하는 함수

- int PQIsEmpty(PQueue* ppq);
  - 우선순위 큐가 빈 경우 TRUE(1)을, 그렇지 않은 경우 FALSE(0)을 반환

- void Penqueue(PQueue* ppq, PQData data);
  - 우선순위 큐에 데이터를 저장한다. 

- PQData Pdequeue(PQueue* ppq);
  - 우선순위가 가장 높은 데이터를 삭제
  - 삭제된 데이터를 반환
  - 본 함수의 호출을 위해서는 데이터가 하나 이상 존재함이 보장 되어야 한다.
    - 먼저 Empty로 확인 후 데이터를 삭제하는 것이 맞다.

