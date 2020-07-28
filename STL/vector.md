# 벡터(Vector)

### 특징

- 임의의 접근 반복자를 지원하는 배열 기반 컨테이너
- 원소가 하나의 메모리 블록에 연속하게 저장되어 있다.
- 배열의 특징인 각 원소로 접근이 빠르다는 장점을 그대로 가지고 있다.
- 원소가 추가되거나 삽입될 때 메모리 재할당이 발생할 수도 있고 상당한 비용을 쓰게 된다.
- 메모리 할당 크기를 알 수 있는 capacity()와 예약할당으로 미리 크게 할당을 할 수 있는 reserve()함수를 제공한다.
- 삽입, 삭제, 반환 같은 것이 빈번하게 발생하는 프로그램이라면 사용하지 않는 것이 좋다.



### 인터페이스

```
Template<typename T, typename Allocator = allocator<T>>
class vector
```

| 생성자        |                                                 |
| ------------- | ----------------------------------------------- |
| vector v      | v는 빈 컨테이너이다.                            |
| vector v(n)   | v는 기본값으로 초기화된 n개의 원소를 갖는다.    |
| vector v(n,x) | v는 x값으로 초기화된 n개의 원소를 갖는다.       |
| vector v(v2)  | v는 v2 컨테이너의 복사본이다.(복사 생성자 호출) |
| vector v(b,e) | v는 반복자 구간[b,e)로 초기화 된 원소를 갖는다. |

| 연산자   |                                                              |
| -------- | ------------------------------------------------------------ |
| v1 == v2 | v1과 v2의 모든 원소가 같은가?(bool 형식)                     |
| v1 != v2 | v1과 v2의 모든 원소 중 하나라도 다른 원소가 있는가?(bool 형식) |
| v1 < v2  | 문자열 비교처럼 v2가 v1보다 큰가? (bool 형식)                |
| v1 <= v2 | 문자열 비교처럼 v2가 v1보다 크거나 같은가?(bool 형식)        |
| v1 > v2  | 문자열 비교처럼 v1이 v2보다 큰가? (bool 형식)                |
| v1 >= v2 | 문자열 비교처럼 v1이 v2보다 크거나 같은가? (bool 형식)       |
| v[i]     | v의 i번째 원소를 참조한다(const, 비 const 버전이 있으며 범위 점검이 없다) |

| 멤버 형식              |                        |
| ---------------------- | ---------------------- |
| allocator_type         | 메모리 관리자 형식     |
| const_iterator         | const 반복자 형식      |
| const_pointer          | Const value_type* 형식 |
| const_reference        | Const value_type&형식  |
| const_reverse_iterator | 두 반복자 차이의 형식  |
| difference_type        | 두 반복자 차이의 형식  |
| iterator               | 반복자 형식            |

| 멤버 함수         |                                                              |
| ----------------- | ------------------------------------------------------------ |
| v.assign(n,x)     | v에 x값으로 n개의 원소를 할당한다.                           |
| v.assign(b, e)    | v를 반복자 구간 [b,e)로 할당한다.                            |
| v.at(i)           | v의 i번째 원소를 참조한다.(const,비 const 버전이 있으며 범위 점검을 포함) |
| v.back()          | v의 마지막 원소를 참조한다.(const, 비 const 버전이 있음)     |
| p=v.begin()       | p는 v의 첫 원소를 가리키는 반복자(const, 비 const 버전이 있음) |
| x=v.capacity()    | x는 v에 할당된 공간의 크기                                   |
| v.clear()         | v의 모든 원소를 제거한다.                                    |
| v.empty()         | v가 비었는지 조사한다.                                       |
| p=v.end()         | p는 v의 끝을 표시하는 반복자다(const, 비 const 버전이 있음)  |
| q=v.erase(p)      | p가 가리키는 원소를 제거한다. q는 다음 원소를 가리킨다.      |
| q=v.erase(b,e)    | 반복자 구간[b,e)의 모든 원소를 제거한다. q는 다음 원소를 가리킨다. |
| v.front()         | v의 첫 번째 원소를 참조하다. (const, 비 const 버전이 있음)   |
| q=v.Insert(p,x)   | p가 가리키는 위치에 x값을 삽입한다. q는 삽입한 원소를 가리키는 반복자. |
| v.Insert(p, n, x) | p가 가리키는 위치에 n개의 c값을 삽입한다.                    |
| v.Insert(p, b, e) | p가 가리키는 위치에 반복자 구간[b,e)의 원소를 삽입한다.      |
| x=v.max_size()    | x는 v가 담을 수 있는 최대 원소의 개수다(메모리의 크기)       |
| v.pop_back()      | v의 마지막 원소를 제거한다.                                  |
| v.push_back(x)    | v의 끝에 x를 추가한다.                                       |
| p=v.regin()       | p는 v의 역 순차열의 첫 원소를 가리키는 반복자다(const, 비 const 버전이 있음) |
| p=v.rend()        | p는 v의 역 순차열의 끝을 표시하는 반복자(const, 비 const 버전이 있음) |
| v.reserve(n)      | n개의 원소를 저장할 공간을 예약한다.                         |
| v.resize(n)       | v의 크기를 n으로 변경하고 확장되는 공간의 값을 기본값으로 초기화 한다. |
| v.resize(n,x)     | v의 크기를 n으로 변경하고 확장되는 공간의 값을 x값으로 초기화 한다. |
| v.size()          | v의 원소의 개수다.                                           |
| v.swap(v2)        | v와 v2를 swap한다.                                           |

#### size() 

size() 메서드와 같은 경우도 음수가 되는 경우가 존재하게 되면 버그를 만들어낼 수 있기 때문에 size()와 같은 메서드를 호출할 때 값을 저장할 변수는 unsigned int타입을 반환 하는 size_type을 쓰는 것을 권장한다. 

```c++
for(vector<int>::size_type i=0; i<v.size(); ++i)
	cout << v[i] << endl;
```

#### size()와 capacity()

size()의 경우는 원소의 갯수를 반환하지만 capacity()의 경우는 다르다. 할당된 공간의 크기를 반환 한다. 데이터가 추가 될 때마다 배열은 크기가 증가해야 하기 때문에 재할당과 원소 복사를 반복하게 되는데 이런 과정을 조금이라도 줄이기 위해 한번 할당 할 때마다 조금 여유(기존 메모리의 * 2)를 가지며 할당을 한다. 그렇기 때문에 size()가 반환하는 값과 capacity()가 반환하는 값은 다를 수 있다. 

#### reserve()

reserve()는 사용 메모리를 예약하는 함수로 메모리를 미리 할당 받았기 때문에 그 범위가 넘어가지 않는 이상 capacity는 reserve를 통해 할당된 크기의 값을 가지고 있다.

#### 생성자에 원소의 크기와 최소값을 지정

 `vector<int> v1(5)`  기본값 0 으로 초기화된 size가 5인 컨테이너이다. 이때 기본값이라는 것은 int의 경우는 0, bool의 경우는 false, 객체의 경우는 NULL을 말한다. 

`vector<int> v2(5,10)` 지정값 10으로 초기화 된 size가 5인 컨테이너

#### resize()

`vector<int> v(5)` 에 10 20 30 40 50 을 넣었을 때

`v.resize(10)`하면 기본값 0으로 초기화된 size가 10인 컨테이너로 확장 되며 출력 했을 때 10 20 30 40 50 0 0 0 0 0 로 출력 된다.

`v.resize(5)`  size가 5인 컨테이너로 축소하게 되면 capacity의 변화는 없다.

#### front()와 back()

front()는 첫 번째 원소를 back()은 마지막 원소를 참조한다. 그리고 front()와 back() 참조를 이용해 원소를 수정할 수도 있다.

`v.front() = 100;`

`v.back() = 500;`

#### []연산자와 at() 멤버

[]연산자는 v[i]와 같은 형태로 i index 원소를 참조할 수 있다. at() 또한 같은 역할을 하는데 그렇다면 []이 아니라 at() 을 권장하는 이유는 뭘까,  at()의 경우는 std::out_of_range 예외를 던져주기 때문이다. 그래서 try catch문과 같이 사용할 수 있다.

```c++
try
{
    cout << v.at(0) << endl;
    cout << v.at(3) << endl;
    cout << v.at(6) 6)<< endl ; //throw out_of_range 예외
}
catch (out_of_range & e)
{
	cout << e.what() << endl
}
```

#### 반복자

```c++
for(vector<int>::iterator iter = v.begin(); iter != v.end(); ++iter)
	cout << *iter << " ";
```

++iter : 반복자를 다음 원소를 가리키도록 이동

*iter : iter가 가리키는 원소를 반환

```c++
iter += 2; // +2한 위치의 원소를 가리킨다
iter -= 1; // -1한 위치의 원소를 가리킨다
```

#### const

`vector<int>::const_iterator`는 const int* 처럼 동작하여 읽기가 가능하지만, `const vector<int>::iterator`은 int* const 처럼 동작하기 때문에 참조의 변형 자체가 안되므로 반복자를 이동할 수 없게 된다.

```c++
vector<int>::iterator iter = v.begin();
vector<int>::const_iterator citer = v.begin();

cout<<*iter<<endl; // 가리키는 원소의 참조
cout<<*citer<<endl; // 가리키는 원소의 상수 참조

cout << *++iter<<endl ; //다음 원소로 이동한 원소의 참조
cout<<**++citer<<endl ; //다음 원소로 이동한 원소의 상수 참조

*iter = 100; // 일반 반복자는 가리키는 원소를 변경할 수 있음
//*citer = 100; // 상수 반복자는 가리키는 원소를 변경할 수 없음

```









> Reference
>
> - SOULSEEK - STL PPT CHAPTER1