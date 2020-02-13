<img src="https://img.shields.io/badge/Update-20.02.03-blue" align = "left">

### 트리(TREE)

트리는 계층적 관계를 표현한 비선형 자료구조로 선형구조는 자료를 저장하고 꺼내는 것에 초점이 맞춰져 있지만 비선형 구조는 저장과 반환, 표현에 초점이 맞춰져있다. 

#### **트리 관련 용어**

- 노드 Node 
- 간선 Edge
- 루트 노드 Root Node
- 단말 노드 Terminal Node / 잎사귀 노드 Leaf Node 
- 내부 노드 Internal Node 
- 부모 노드
- 자식 노드
- 형제 Sibling
- 레벨 
- 높이 
- 서브 트리 Sub-Tree 

#### **이진 트리**

자식이 두 개씩 달린 트리를 이진 트리라고 한다. 노드가 위치할 수 있는 곳에 노드가 존재하지 않는다면, 공집합 노드가 존재하는 것으로 생각한다. 이 공집합을 포함해서 이진 트리 노드인지 함께 판단한다.

**이진 트리의 종류**

- 포화 이진 트리 Perfect binary tree
- 완전 이진 트리 Complete binary tree
- 정 이진 트리 Full binary tree

**이진 트리의 속성** (노드의 수 / 높이 등의 공식)

**이진 트리 탐색**

- 전위 순회
- 중위 순회
- 후위 순회

**표현 방법**

- 배열
- 연결리스트 

> 참고 사이트
>
> https://monsieursongsong.tistory.com/6
>
> https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html
>
> [ Wiki](https://ko.wikipedia.org/wiki/이진_트리)
>
> PPT 자료

**과제**

이진 트리에서 소멸과 관련된 함수를 작성해보자.



<img src="https://img.shields.io/badge/Update-20.02.13-blue" align = "left">

### 이진트리 순회(Traversal)

- **전위 순회 Preorder Traversal**
  - Root -> Reft -> Right (부모 노드 -> 왼쪽 자식 노드 -> 오른쪽 자식 노드)
- **중위 순회 Inorder Traversal**
  - Reft -> Root -> Right (왼쪽 자식 노드 -> 부모노드 -> 오른쪽 자식 노드)
- **후위 순회 Postorder Traversal**
  - Reft -> Right -> Root (왼쪽 자식 노드 -> 오른쪽 자식 노드 -> 부모 노드)

