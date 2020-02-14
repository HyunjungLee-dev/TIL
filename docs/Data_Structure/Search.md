## 탐색의 이해와 보간 탐색

### 탐색의 이해

- 효율적인 탐색을 위해서 검색방법을 고민하는 것보다 **효율적으로 저장을 하면 탐색도 효율적이게 된다.**
- 자료구조에서 탐색은 중요한 위치를 차지하고 있다.

### 순차 탐색 (Sequential Search)

- 배열의 처음부터 끝까지 차례대로 비교하여 원하는 데이터를 찾아낸다.
- **단순하지만 비효율적**
- 단방향으로 탐색을 수행하기 때문에 **선형 탐색(Linear Search)**라고 부르기도 한다.
- 시간 복잡도 O(n)

### 이진 탐색  (Binary Search)

- 순차 탐색 알고리즘보다 좋은 성능을 발휘한다.
- **배열이 정렬이 되어 있어야한다.**
- 배열 처음과 끝을 합해서 반으로 나누고 가운데 원소 값을 알아와서 정렬한 기준을 근거로 비교해서 어디서 원하는 값을 찾을지 판단하고 계속 그렇게 반으로 나누면서 탐색한다.
  - 한번 비교를 거칠때 탐색 범위가 반(1/2)으로 줄어든다.
- C++ STL에서 라이브러리로 제공
- 시간 복잡도 O(log₂n)

### 보간 탐색 (Interpolation Search)

- 이진 탐색과 비슷하지만 탐색 시작위치에서 차이가 있다.
  - 이진 탐색은 반으로 나누어 찾지만 보간 탐색의 경우 인덱스의 위치를 예측해서 그 부분 부터 탐색한다.
- 탐색하고자 하는 인덱스의 위치에 최대한 가까운 곳부터 검색을 해서 탐색 대상을 줄이는 방법이다.
- 지정된 대상과 찾을 인덱스의 위치가 가까울 수록 시간이 줄어들고 최악의 경우라도 일정 이상의 인덱스 탐색 대상이 줄어들게 된다. 이진 탐색과 같은 시간 복잡도를 가지지만 많은 데이터가 비교적 균등하게 분포되어 있는 자료의 경우 훨씬 효율적인 방법이다.
  - 평균적으로 O(log₂n)
  - 최악의 경우 O(n) 의 시간 복잡도를 보인다.
- 사전과 전화번호부에 비교 할 수 있다.
  - 감자라는 단어를 사전에서 찾을 때 'ㄱ' 에서 찾아가는 것과 같은 것

### 이진 탐색 트리(Binary Search Tree)

이진 탐색이 적용된 이진 트리

**이진 탐색 트리의 특성**

*이진 트리의 특성도 포함되어 있다.*

- 노드에 저장된 키는 유일하다.
- 루트 노드의 키가 왼쪽 서브 트리를 구성하는 어떠한 노드의 키보다 크다.
- 루트 노드의 키가 오른쪽 서브 트리를 구성하는 어떠한 노드의 키보다 작다.
- 왼쪽과 오른쪽 서브 트리도 이진 탐색 트리이다.
- 서브 노드 안에서 부모 자식 관계에서도 규칙이 적용 되어야 한다.
- 왼쪽 자식 노드의 키 < 부모 노드의 키 < 오른쪽 자식 노드의 키

> 참조 사이트
>
> - PPT CHAPTER 3
> - PPT CHAPTER 5
>
> - https://blog.hexabrain.net/246
> - http://suyeongpark.me/archives/2328

**과제**

수 입력 받고 탐색 결과를 보여주는 BinarySearchTreeMain.cpp를 만들어보자.



#### 이진 탐색 트리 삭제 알고리즘

```c
BTreeNode * BSTRemove(BTreeNode ** pRoot, BSTData target)
{
	// 삭제 대상이 루트 노드인 경우를 별도로 고려해야 한다.

	BTreeNode * pVRoot = MakeBTreeNode();    // 가상 루트 노드;

	BTreeNode * pNode = pVRoot;    // parent node
	BTreeNode * cNode = *pRoot;    // current node
	BTreeNode * dNode;    // delete node

	// 루트 노드를 pVRoot가 가리키는 노드의 오른쪽 서브 노드가 되게 한다.
	ChangeRightSubTree(pVRoot, *pRoot);

	// 삭제 대상을 저장한 노드 탐색
	while (cNode != NULL && GetData(cNode) != target)
	{
		pNode = cNode; // pNode가 삭제 대상의 부모노드를 가리킨다.

		if (target < GetData(cNode))
			cNode = GetLeftSubTree(cNode);
		else
			cNode = GetRightSubTree(cNode);
	}

	if (cNode == NULL)    // 삭제 대상이 존재하지 않는다면,
		return NULL;

	dNode = cNode;    // 삭제 대상을 dNode가 가리키게 한다.

```

**첫 번째 경우** : 삭제할 노드가 단말 노드인 경우

```C
// 첫 번째 경우: 삭제할 노드가 단말 노드인 경우
	if (GetLeftSubTree(dNode) == NULL && GetRightSubTree(dNode) == NULL)
	{
		if (GetLeftSubTree(pNode) == dNode) // 삭제할 노드가 왼쪽 자식 노드라면,
			RemoveLeftSubTree(pNode);//왼쪽 자식 노드 트리에서 제거
		else  // 삭제할 노드가 오른쪽 자식 노드라면,
			RemoveRightSubTree(pNode); // 오른쪽 자식 노드 트리에서 제거
	}
```

단말 노드를 삭제 하는 것은 세가지의 경우 중 가장 간단하다. 삭제 할 노드가 왼쪽과 오른쪽 각각 서브 트리가 없는 경우 즉 단일 노드일 경우는 삭제할 할 노드가 부모 노드의 왼쪽인지 오른쪽인지 확인하고  Remove 함수를 통해 해당 노드를  NULL로 만들어 연결을 끊어준다. 동적 할당 되어 있을 경우는 메모리를 반납하고 NULL 로 만들어주면 된다.



**두 번째 경우** : 하나의 자식 노드를 갖는 경우

```c
// 두 번째 경우: 하나의 자식 노드를 갖는 경우
	else if (GetLeftSubTree(dNode) == NULL || GetRightSubTree(dNode) == NULL)
	{
		BTreeNode * dcNode;    // delete node의 자식 노드
       // 삭제 대상의 자식 노드를 찾는다.
		if (GetLeftSubTree(dNode) != NULL) // 자식 노드가 왼쪽에 있다면,
			dcNode = GetLeftSubTree(dNode);
		else                              // 자식 노드가 오른쪽에 있다면,
			dcNode = GetRightSubTree(dNode);
       // 삭제 대상의 부모 노드와 자식 노드를 연결한다.
		if (GetLeftSubTree(pNode) == dNode) // 삭제 대상이 왼쪽 자식 노드이면,
			ChangeLeftSubTree(pNode, dcNode);//왼쪽으로 연결
		else                                // 삭제 대상이 오른쪽 자식 노드이면,
			ChangeRightSubTree(pNode, dcNode); // 오른쪽으로 연결
	}
```

이 경우에는 첫 번째 경우와 다른 점은 else if의 조건 부터 알 수 있는데 하나의 자식 노드를 갖는 경우 이기 때문에 첫 번째 경우는 &&이었지만 지금은 || 이라는 것을 먼저 확인 할 수 있고, 그렇다면 자신 노드가 있다는 것이기에 이 경우에는 삭제할 노드의 부모 노드와 자식 노드를 연결 시켜줘야하기 때문에 먼저 dNode(삭제 노드)의 자식이 왼쪽이냐 오른쪽이냐를 구분 하여 dcNode에 주소를 넣어주고 dNode(삭제 노드)가 삭제 노드의 부모노드의 왼쪽이냐 오른 쪽이냐를 확인해주고  pNode의 오른쪽 혹은 왼쪽에 dcNode(삭제노드의 자식)을 연결 시켜주면 된다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              

**세 번째 경우** : 두 개의 자식 노드를 모두 갖는 경우

```c
// 세 번째 경우: 두 개의 자식 노드를 모두 갖는 경우
	else
	{
		BTreeNode * mNode = GetRightSubTree(dNode);    // mininum node
		BTreeNode * mpNode = dNode;    // mininum node의 부모 노드
		int delData;

		// 삭제할 노드를 대체할 노드를 찾는다.
		while (GetLeftSubTree(mNode) != NULL)
		{
			mpNode = mNode;
			mNode = GetLeftSubTree(mNode);
		}

		// 대체할 노드에 저장된 값을 삭제할 노드에 대입한다.
		delData = GetData(dNode);    // 대입 전 데이터 백업
		SetData(dNode, GetData(mNode)); // 대입

		// 대체할 노드의 부모 노드와 자식 노드를 연결한다.
		if (GetLeftSubTree(mpNode) == mNode) // 대체 노드가 왼쪽 자식 노드라면,
			ChangeLeftSubTree(mpNode, GetRigtSubTree(mNode));
		else                                // 대체 노드가 오른쪽 자식 노드라면,
			ChangeRightSubTree(mpNode, GetRightSubTree(mNode));

		dNode = mNode; // 떨어져 나간 노드가 dNode
		SetData(dNode, delData);    // 백업 데이터 복원
	}
```

위의 두 경우는 그냥 NULL로 해주거나 간단히 연결 시켜주는 것으로 끝났는데 세 번째 경우는 가장 복잡한 경우이다. 삭제 하려는 노드가 두 개의 서브트리를 가지고 있는 경우 이다. 이 경우에는 왼쪽 서브트리에 있는 값 중 가장 큰 값, 혹은 오른쪽 서브트리에 있는 값중 가장 작은 값을 가지고 있는 노드를 연결 시켜주면 된다.

그렇다면 왜 왼쪽 서브트리는 가장 큰 값이고 오른쪽 서브트리는 가장 작은 값일까? 그것은 트리의 변동성을 최소화하기 위해서이다. 중위 순회를 한다고 가정할때 순회 순서는 L - V - R 이다. 왼쪽 서브 트리의 경우 R 이 오른쪽 서브트리의 경우  L이 삭제할 노드의 중위 선행자 후속자에 속하기 때문에 이들로 대체를 하면 변동성을 최소화 할 수 있다.

 그렇다면 삭제하는 과정을 단계별로 살펴보자.

1. 삭제할 노드를 대체할 노드를 찾는다.(위의 기준에 근거하여)
2. 대체할 노드에 저장된 값을 삭제할 노드에 대입한다.
3. 대체할 노드의 부모 노드와 자식 노드를 연결한다.

예를 들어 삭제할 노드의 오른쪽 서브트리에서 가장 작은 값을 지니는 노드를 찾아서 이것으로 삭제할 노드를 대체 할 경우, 가장 작은 값을 지니는 노드를 찾으려면 NULL을 만날 때까지 왼쪽 자식 노드를 계속해서 이동해야한다. 그렇게 찾아낸 값을 삭제 노드의 부모와 이어주고 삭제 노드의 자식 노드들과 연결해준다.

**삭제된 누드가 루트 노드인 경우**

```c
// 삭제된 노드가 루트 노드인 경우에 대한 처리
	if (GetRightSubTree(pVRoot) != *pRoot)
		*pRoot = GetRightSubTree(pVRoot);// 루트 노드이 변경을 반영

	free(pVRoot); // 가상 루트노드의 소멸
	return dNode; // 삭제 대상의 반환
```



> 참고 사이트
>
> https://mattlee.tistory.com/30?category=683544
>
> https://hongku.tistory.com/160
>
> http://blog.naver.com/ckkg45/220599534697
