# 덱(Deque)

### 특징

- 배열 기반의 컨테이너이다.
- [임의의 접근 반복자](https://hyunjung-til.netlify.com/#/STL/STL?id=반복자의-범주)를 지원한다.
- [vector](https://hyunjung-til.netlify.com/#/STL/vector)와 다르게 원소가 메모리 블록 한군데가 아닌 여러 블록으로 나뉘어 저장된다.
- 앞쪽과 뒤쪽으로 모두 추가, 삭제 할 수 있다.

### 인터페이스

템플릿 형식

```c++
Template<typenam T, typename Allocator = allocator<T>>
class deque
```

| 생성자         |                                                    |
| -------------- | -------------------------------------------------- |
| Deque dq       | Dq는 빈 컨테이너이다.                              |
| Deque dq(n)    | Dq는 기본값으로 초기화된 n개의 원소를 갖는다.      |
| Deque dq(n, x) | Dq는 x값으로 초기화된 n개의 원소를 갖는다.         |
| Deque dq(dq2)  | Dq는 dq2 컨테이너의 복사본이다. (복사 생성자 호출) |
| Deque dq(b, e) | Dq는 반복자 구간 [b,e) 로 초기화된 원소를 갖는다.  |

| 연산자     |                                                              |
| ---------- | ------------------------------------------------------------ |
| dq1 == dq2 | dq1과 dq2의 모든 원소가 같은가? (bool 형식)                  |
| dq1 != dq2 | dq1과 dq2의 모든 원소 중 하나라도 다른 원소가 있는가? (bool 형식) |
| dq1 < dq2  | 문자열 비교처럼 dq2가 dq1보다 큰가? (bool 형식)              |
| dq1 <= dq2 | 문자열 비교처럼 d2가 dq1 보다 크거나 같은가?(bool 형식)      |
| dq1 > dq2  | 문자열 비교처럼 dq1이 dq2보다 큰가?(bool 형식)               |
| dq1 >= dq2 | 문자열 비교처럼 dq1이 dq2보다 크거나 같은가?(bool 형식)      |
| dq[i]      | sq의 i번째 원소를 참조한다(const, 비 const 버전이 있으며 범위 점검이 없음) |

| 멤버 형식              |                                     |
| ---------------------- | ----------------------------------- |
| allocator_type         | 메모리 관리자 형식                  |
| const_iterator         | const 반복자 형식                   |
| const_pointer          | const value_type* 형식              |
| const_reference        | const value_type& 형식              |
| const_reverse_iterator | const 역 반복자 형식                |
| defference_type        | 두 반복자 차이의 형식               |
| iterator               | 반복자 형식                         |
| pointer                | value_type* 형식                    |
| reference              | value_type& 형식                    |
| reverse_iterator       | 역 반복자 형식                      |
| size_type              | 첨자(index)나 원소의 개수 등의 형식 |
| value_type             | 원소의 형식                         |

| 멤버 함수          |                                                              |
| ------------------ | ------------------------------------------------------------ |
| dq.assign          | dq에 x값으로 n개의 원소를 할당한다.                          |
| dq.assign(b, e)    | dq를 반복자 구간[b,e)로 할당한다.                            |
| dq.at(i)           | dq의 i번째 원소를 참조한다.(const, 비 const 버전이 있으며 범위 점검 포함) |
| dq.back()          | dq의 마지막 원소를 참조한다. (const, 비 const 버전이 있음)   |
| P=dq.begin()       | p는 dq의 첫 원소를 가리키는 반복자다(const, 비 const 버전이 있음) |
| dq.clear()         | dq의 모든 원소를 제거한다.                                   |
| dq.empty()         | dq가 비었는지 조사한다.                                      |
| p=dq.end()         | p는 dq의 끝을 표시하는 반복자다(const,  비 const 버전이 있음) |
| q=dq.erase(p)      | p가 가리키는 원소를 제거한다. q는 다음 원소를 가리킨다.      |
| q=dq.erase(b,e)    | 반복자 구간[b,e)의 모든 원소를 제거한다. q는 다음 원소를 가리킨다. |
| dq.front()         | dq의 첫 번째 원소를 참조한다.(const, 비 const 버전이 있음)   |
| q=dq.insert(p, x)  | p가 가리키는 위치에 x값을 삽입한다. q는 삽입한 원소를 가리키는 반복자 |
| dq.insert(p, n, x) | p가 가리키는 위치에 n개의 x값을 삽입한다.                    |
| dq.insert(p, b, e) | p가 가리키는 위치에 반복자 구간 [b,e)의 원소를 삽입한다.     |
| x=dq.max_size()    | x는 dq가 담을 수 있는 최대 원소의 개수(메모리의 크기)다.     |
| dq.pop_back()      | dq는 마지막 원소를 제거한다.                                 |
| dq.pop_front()     | dq의 첫 원소를 제거한다.                                     |
| dq.push_back(x)    | dq의 끝에 x를 추가한다.                                      |
| dq.push_front(x)   | dq의 앞쪽에 x를 추가한다.                                    |
| p=dq.rbegin()      | p는 dq의 역 순차열의 첫 원소를 가리키는 반복자다.            |
| p=dq.rend()        | p는 dq의 역 순차의 끝을 표시하는 반복자다.                   |
| dq.rsize(n)        | dq의 크기를 n으로 변경하고 확장되는 공간의 값을 기본값으로 초기화한다. |
| dq.size()          | dq의 원소의 개수다.                                          |
| dq.swap(dq2)       | dq와 dq2를 swap 한다.                                        |

#### vector와 deque의 비교

vector와 deque의 동작 결과 자체는 다른 점이 없다. 예를들어 동일한 값으로 초기화한 n개의  원소를 갖는 벡터 컨테이너, 덱 컨테이너가 있다고 했을 때  push_back()을 통해 같은 값의 원소를 추가해준 후 조회를 하여 최종적으로 출력 되는 값은 동일하다. 하지만 여기서 비교를 하는 것은 동작 결과가 아닌 동작을 어떻게 하는가에 대해서 생각해볼 필요가 있다.

vector의 경우 할당이 넘어서면 원소들을 재할당한 뒤 복사를 하지만 deque의 경우는 새로 추가 할당만 하고 새로운 원소만 추가한다. 이러한 부분에서 차이가 있다고 할 수 있다.

#### push_back()

push가 붙은 함수는 원소를 추가하는 함수이다. 이때 push_back()의 경우는 덱의 끝에 원소를 추가한다. 앞서 자료구조를 공부 했을 때 head와 tail이 있었는데 tail에 원소를 추가한다고 생각하면 된다.

```c++
void main()
{
    deque<int>dq; 
    
    for(deque<int>::size_type i=0; i<10; ++i)
        dq.push_back((i+1) * 10);
    
    for(deque<int>::size_type i=0; i<dq.size(); ++i)
        cout<<dq[i]<<'';
    cout<<endl;
}
```

```
//출력 결과
10 20 30 40 50 60 70 80 90 100
```



#### push_front()

push_front()의 경우는 덱의 앞쪽에 원소를 추가한다. 앞서 자료구조를 공부 했을 때 head와 tail이 있었는데 head에 원소를 추가한다고 생각하면 된다.

```c++
void main()
{
    deque<int>dq;
    
    for(deque<int>::size_type i=0; i<10; ++i)
        dq.push_front((i+1) * 10);
    
    for(deque<int>::size_type i=0; i<dq.size(); ++i)
        cout<<dq[i]<<'';
    cout<<endl;
}
```

```
//출력 결과
100 90 80 70 60 50 40 30 20 10
```



#### 반복자

deque의 반복자 사용의 예이다. 

```c++
void main()
{
    deque<int> dq;
    
    dq.push_back(10);
    dq.push_back(20);
    dq.push_back(30);
    dq.push_back(40);
    dq.push_back(50);
    
    deque<int>::iterator iter;
    for(iter = dq.begin(); iter!=dq.end(); ++iter)
        cout << *iter << " ";
    
    cout<<endl;
    
    iter = dq.begin()+2;
    cout << *iter << endl;
    
    iter += 2;
    cout << *iter << endl;
    
    iter -= 3;
    cout << *iter << endl;
}
```

```
//출력 결과
10 20 30 40 50
30
50 
20
```

*iter : iter가 가리키는 원소를 반환

++iter : 반복자를 다음 원소를 가리키도록 이동

iter = begin() + n : begin() (첫 원소를 가리키는 반복자 ) + n한 위치의 원소를 가리킨다

iter += n : +n한 위치의 원소를 가리킨다.

iter -= n : -n 한 위치의 원소를 가리킨다.

#### insert()

```c++
void main()
{
    deque<int> dq;
    
    for(int i = 0; i<10; i++)
        dq.push_back((i+1)*10);
    
    deque<int>::iterator iter;
    deque<int>::iterator iter2;
    
    for(iter = dq.begin(); iter != dq.end(); ++iter)
        cout<<*iter<<'';
    
    cout << endl;
    
    iter = dq.begin()+2;
    iter2 = dq.insert(iter, 500);
    cout << *iter2 <<endl;
    
    for(iter = dq.begin(); iter!=dq.end(); ++iter)
        cout<<*iter<<'';
    
    cout << endl;
}
```

```
//출력 결과
10 20 30 40 50 60 70 80 90 100
500
10 20 500 30 40 50 60 70 80 90 100
```

q=dq.insert(p, x)는 p가 가리키는 위치에 x값을 삽입한다. q는 삽입한 원소를 가리키는 반복자이다.

위의 예제를 보면 `iter = dq.begin()+2`  세번째 자리에 위치한 원소를 가리킨다. `iter2 = dq.insert(iter, 500);`  그 위치에 500을 삽입하는 것이다. 그랬을 경우 출력 결과와 같이 500이 들어가게 된다.





> Reference
>
> - SOULSEEK - STL PPT CHAPTER1

