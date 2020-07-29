## 버블 정렬(Bubble Sort)

**버블 정렬의 개념**

- 인접한 두 개의 데이터를 비교해가면서 정렬을 진행하는 방식
- 정렬 순서상 위치가 바뀌어야 하는 경우에  정한 기준으로 값을 뒤로 넘겨 두 데이터의 위치를 바꿔 나간다.

- 비교를 반복하면서 자리를 이동하는 모양이 거품 같다고 해서 버블정렬

버블 정렬의 경우 인접한 두 개의 데이터를 비교하여 기준에 따라 위치를 바꿔나게 되는데 한번의 순회가 있으면 예를들어 오름차순의 경우에는 가장 큰 숫자가 마지막에 위치하게 되는데 그렇기 때문에 다음 순회부터는 모든 데이터를 비교 할 필요가 없다. 이미 큰 수는 정렬이 되어있기 때문에 즉, 과정을 반복할때마다 이미 정렬된 데이터가 있을 것이고 그것을 제외한 데이터만 비교하면 된다는 것이다.

**버블 정렬의 시간 복잡도**

- 비교 횟수

반복 할 수록 수가 점점 작아지게 된다. n개의 데이터가 있다고 했을 때 n-1번 반복 하면 정렬이 끝다게 된다. 즉 4개의 데이터가 있을때 3 + 2 + 1 해서 총 6번을 비교하게 된다.  식으로 나타내면

 `(n-1) + (n-2)+... + 2 + 1 = (n-1) * n/2 = n(n-1)/2`  즉 등차수열의 합에 해당하게 된다. 

- 이동 횟수 
  - 최선의 경우 : 이미 정렬된 원소들이 주어진 경우
  - 최악의 경우 : 역순으로 정렬 된 원소들이 주어진 경우 , 비교 횟수와 같은 `n(n-1)/2`

비교 횟수, 이동 횟수 모두 최악의 경우에는 3배 가량 많은 시간을 소모하지만 빅-오에서는 제외한다. 

**정리**
버블 정렬의 경우 O(n²)라는 시간복잡도로 굉장히 느린 편에 속하는 정렬 알고리즘이기에 비교할 데이터가 많을 수록 성능이 저하 되기 때문에 코드가 단순하여 구현하기 좋고 이해가 쉽다하여도 데이터의 개수가 적은 경우에   주로 사용한다.

## 선택정렬 (Selection Sort)

**선택 정렬의 개념** 

- 정렬 순서상 가장 앞서는 것(우선 순위 중 가장 높은 요소)을 선택해서 가장 왼쪽으로 이동시키고, 원래 그 자리에 있던 데이터는 빈 자리에 가져다 놓는다.
- 임의의 빈자리를 마련해 놓아야 한다.

**선택 정렬의 시간 복잡도**

- 비교 횟수

선택 정렬은 순환을 할수록 비교 횟수가 줄어든다. 순환 하면서 우선 순위가 높은 것을 이미 옮겼기 때문에 원소가 8개 이면 7번 비교, 6번 비교, 5번 비교 ... 8번째에는 0번의 비교 연산이 일어난다. 버블 정렬과 같이 총  7+6 +5 + 4 +...+ 1 + 0 번을 비교하게 되는 것이다.  

  `(n-1) + (n-2)+... + 2 + 1 = (n-1) * n/2 = n(n-1)/2`  

- 교환 횟수

한번 교환 하기 위하여 3번의 이동(SWAP 함수의 작업)이 필요하므로 3(n-1)번

`T(n) = (n-1) + (n-2) + … + 2 + 1 = n(n-1)/2 = O(n^2)`

**정리**

자료 이동 횟수가 미리 결정 되는 장점이 있지만 안정성을 만족하지 않는데 즉, 값이 같은 레코드가 있는 경우에는 상대적인 위치가 변경될 수 있다.



## 삽입 정렬(Insertion Sort)

**삽입 정렬의 개념** 

- 첫 번째와 두 번째를 비교한 후 그 다음 데이터의 위치가 속할 곳을 찾아서 데이터를 밀어내고 삽입되는 정렬 방식이다.
- 정렬이 완료된 영역의 다음에 위치한 데이터가 그 다음 정렬 대상이다.
- 삽입할 위치를 발견하고 데이터를 한 칸씩 밀수도 있지만, 데이터를 한 칸씩 밀면서 삽입할 위치를 찾을 수도 있다.

**선택정렬과 삽입정렬의 차이**

- 선택정렬
  - 우선 순위가 높은걸 차례대로 가져와서 집어 넣음
  - 선택하는 순간에 정렬 알고리즘이 적용됨
- 삽입정렬
  - 기준을 잡아놓고 맞는 자리로 데이터를 집어 넣으며 정렬
  - 데이터를 삽입하는 과정에 정렬 알고리즘이 적용됨

**삽입 정렬의 시간 복잡도**

- 비교 연산과 이동 연산 모두 이중 반복문 안쪽에 있다. O(n²)
- 비교 횟수
  - 외부 루프 안의 각 반복마다 i번 비교 수행
  - `(n-1) + (n-2)+... + 2 + 1 = (n-1) * n/2 = n(n-1)/2` =   O(n²)
    - 버블정렬과 다를 것이 없지만 버블정렬은 무조건 n(n-1)/2회 이지만 삽입 정렬은 데이터의 집합이 정렬 되어 있는 경우, 한번도 비교를 거치지 않는다. 
  - 최선의 경우와 최악의 경우에 비교 횟수 평균을 내면 n²+n-1 / 2
- 교환 횟수
  - 외부 루프의 각 단계마다 (i+2)번의 이동 발생
  - n(n-1)/2 + 2(n-1) = (n^2 + 3n -4) / 2 = O(n²)

**정리**

안정한 정렬 방법이며 레코드의 수가 적을 경우 알고리즘이 간단하여 다른 복잡한 정렬 방법 보다 유리할 수 있으며 레코드가 정렬이 되어 있는 경우 매우 효율적일 수 있다. 하지만 비교적 많은 레코드들의 이동을 포함하기에 레코드 수가 많고 레코드 크기가 클 경우에 적합하지 않다.

> **참고 사이트**
>
> - https://seongkyun.github.io/data_structure/2019/08/10/data_structure/
> - PPT CHAPTER 5
> - 버블정렬
>   - https://bowbowbow.tistory.com/10
>   - https://steemit.com/kr-dev/@heejin/bubble-sort
> - 선택 정렬
>   - https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html
> - 삽입 정렬
>
>   - https://hannom.tistory.com/39
>   - https://gmlwjd9405.github.io/2018/05/06/algorithm-insertion-sort.html

**추가 공부 내용**

- 정렬 개념
- 정렬 방법의 분류
  - 정렬의 실행 방법에 따른 분류
    - 비교식 정렬(Comparative Sort)
    - 분산식 정렬(Distribute Sort)
  - 정렬 장소에 따른 분류
    - 내부 정렬(Internal Sort)
    - 외부 정렬(External Sort)



**안정 정렬(Stable Sort) **

동일한 값에 대한 기존의 순서가 유지되는 정렬 방식

**불안정 정렬(Unstable Sort)**

동일한 값에 대해 기존의 순서가 뒤바뀔 수 있는 정렬 방식



## 힙 정렬(Heap Sort)

**힙 정렬의 개념**

- 힙의 특성을 살린 알고리즘(힙에 대한 개념 필요)
- 최댓값, 최솟값을 쉽게 추출할 수 있는 자료구조

**힙 정렬의 시간 복잡도**

Best-case : nlog₂n

Average-case :nlog₂n

Worst - case : nlog₂n

Memory : 1

stable : no

**정리**

시작 복잡도가 좋은 편이며 전체 자료를 정렬하는 것이 아니라 가장 큰 값 몇개만 필요할 때 가장 유용하다.



## 병합 정렬(Merge Sort)

**병합 정렬의 개념**

- 분할 정복(divide and conquer)이라는 알고리즘 디자인 기법에 근거하여 만들어진 정렬 방법.
  - 분할 정복 방법
    - 1단계 : 분할(Divide) - 해결이 용이한 단계까지 문제를 분할해 나간다.
    - 2단계 : 정복(Conquer) - 해결이 용이한 수준까지 분할된 문제를 해결한다.
    - 3단계 : 결합(Combine) - 분활해서 해결한 결과를 결합하여 마무리한다.

**병합 정렬의 과정**

- 둘로 나누는 것보다 1개의 데이터가 남을 때까지 나눠서 정렬을 하고 다시 합치는 과정이 더 중요하다.
  - 실제로 정렬이 이루어지는 시점은 합병(merge)하는 단계
- 나눠질 수 없을 만큼 나눴다가 정렬을 한 후 병합을 진행한다.
- 나누는 과정의 순서대로 다시 병합을 하기 때문에 나누는 과정과 합치는 과정의 횟수는 같다.
- 재귀적 구현을 위한 방법이다.
- 병합 정렬의 단계
  - 분할 : 입력 배열을 같은 크기의 2개의 부분 배열로 분할한다.
  - 정복 : 부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작으면 순환 호출을 이용하여 다시 분할 정복 방법을 적용한다.
  - 결합 : 정렬된 부분 배열들을 하나의 배열에 합병한다.

**병합 정렬의 시간 복잡도**

 K = 𝐥𝐨𝐠𝟐 𝒏 ➔ O(𝐧𝒍𝒐𝒈𝟐 𝒏)



## 퀵 정렬(Quick Sort)

**퀵 정렬의 개념**

- Pivot이라는 중심 값을 기준으로 두 자료의 키 값을 비교하여 위치를 교환하는 정렬 방식
- Pivot의 위치 교환이 끝난 다음, 기존 자료 집합을  Pivot을 기준으로 2개의 부분 집합으로 나누고, 분할된 부분 집합에 대해 다시 퀵 정렬을 실행하는 방식으로 진행된다.
- 분할 정복 알고리즘의 하나로, 평균적으로 매우 빠른 수행 속도를 자랑하는 정렬 방법

**참고 사이트**

- [알고리즘 애니메이션](http://www.algostructure.com/sorting/heapsort.php)
- [Heee's Development Blog](https://gmlwjd9405.github.io/2018/05/10/algorithm-heap-sort.html)
- [Merge Sort Animation](https://www.youtube.com/watch?v=dxuIwsPKRts)
- https://ko.khanacademy.org/computing/computer-science




