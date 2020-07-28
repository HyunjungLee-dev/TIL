# 리스트(List)

### 특징

- 노드 기반의 컨테이너
- 이중 연결 리스트 기반
- 인덱스 접근 연산자를 지원하지 않는다.
- 다른 list와 결합할 때 좋은 컨테이너
- 순차열 중간에 삽입, 제거가 빈번하게 발생하며 원소의 상대적인 순서가 중요하면 list 컨테이너를 사용한다.

### vector와 list의 차이

|                      | vector | list |
| -------------------- | ------ | ---- |
| 크기 변경 가능       | O      | O    |
| 중간 삽입, 삭제 용이 | X      | O    |
| 순차 접근 가능       | O      | O    |
| 랜덤 접근 가능       | O      | X    |

vector와  list의 차이점은 크게 2가지로 중간 삽입, 삭제 부분과 랜덤 접근 부분이다. 

중간 삽입, 삭제가 없고 랜덤 접근을 자주 해야 된다면 vector가 좋고, 중간 삽입, 삭제가 자주 있으며 랜덤 접근이 필요 없으면 list가 좋다.

### 간단 주요 함수 정리

- push_front()  / push_back() : 추가
- pop_front() / pop_back() : 제거
- insert() : 삽입
- erase() : 제거
- spice() : 잘라 붙이기
- merge() : 합병 정렬
- unique() : 중복 원소 제거
- sort() : 정렬
- remove() : 원소 제거(값)

### 인터페이스

템플릿 형식

```c++
Template<typename T, typename Allocator = allocator<T>>
class list
```

| 생성자         |                                                  |
| -------------- | ------------------------------------------------ |
| list lt        | lt는 빈 컨테이너                                 |
| list lt(n)     | lt는 기본값으로 초기화된 n개의 원소를 갖는다.    |
| list lt(n, x)  | lt는 x 값으로 초기화된 n개의 원소를 갖는다.      |
| list lt(lt2)   | lt는 lt2 컨테이너의 복사본이다(복사 생성자)      |
| list lt(b , e) | lt는 반보자 구간(b, e)로 초기화된 원소를 갖는다. |

| 연산자     |                                                              |
| ---------- | ------------------------------------------------------------ |
| Lt1 == lt2 | Lt1과 lt2의 모든 원소가 같은가? (bool 형식)                  |
| Lt1 != lt2 | Lt1과 lt2의 모든 원소 중 하나라도 다른 원소가 있는가?(bool 형식) |
| Lt1 < lt2  | 문자열 비교처럼 lt2가 Lt1보다 큰가? (bool 형식)              |
| Lt1 <= lt2 | 문자열 비교처럼 lt2가 Lt1보다 크거나 같은가?(bool 형식)      |
| Lt1 > lt2  | 문자열 비교처럼 lt1이 Lt2보다 큰가? (bool 형식)              |
| Lt1 >= lt2 | 문자열 비교처럼 Lt1이 lt2보다 크거나 같은가?(bool 형식)      |

| 멤버 형식              |                                     |
| ---------------------- | ----------------------------------- |
| allocator_type         | 메모리 관리자 형식                  |
| const_iterator         | const 반복자 형식                   |
| const_pointer          | const value_type* 형식              |
| const_reference        | const value_type& 형식              |
| const_reverse_iterator | const 역 반복자 형식                |
| difference_type        | 두 반복자 차이의 형식               |
| iterator               | 반복자 형식                         |
| pointer                | value_type* 형식                    |
| reference              | value_type& 형식                    |
| reverse_iterator       | 역 반복자 형식                      |
| size_type              | 첨자(index)나 원소의 개수 등의 형식 |
| value_type             | 원소의 형식                         |

| 멤버 함수            |                                                              |
| -------------------- | ------------------------------------------------------------ |
| lt.assign(n,x)       | lt값에 x값으로 n개의 원소를 할당한다.                        |
| lt.assign(b,e)       | lt를 반복자 구간 [b,e)로 할당한다.                           |
| lt.back()            | lt의 마지막 원소를 참조한다.(const, 비 const 버전 있음)      |
| p=lt.begin()         | p는 lt의 첫 원소를 가리키는 반복자다.(const, 비 const 버전 있음) |
| lt.clear()           | lt의 모든 원소를 제거한다.                                   |
| lt.empty()           | lt가 비었는지 조사한다.                                      |
| p=lt.end()           | p는 lt의 끝을 표시하는  반복자다.(const, 비 const 버전 있음) |
| q = lt.erase(p)      | p가 가리키는 원소를 제거한다. q는 다음 원소를 가리킨다.      |
| q = lt.erase(b,e)    | 반복자 구간[b,e)의 모든 원소를 제거한다. q는 다음 원소다.    |
| lt.front()           | lt의 첫 번째 원소를 참조한다(const, 비 const 버전 있음)      |
| q=lt.insert(p,x)     | p가 가리키는 위치에 x값을 삽입한다. q는 삽입한 원소를 가리키는 반복자다. |
| lt.insert(p,n,x)     | p가 가리키는 위치에 n개의 x값을 삽입한다.                    |
| lt.insert(p,b,e)     | p가 가리키는 위치에 반복자 구간[b,e)의 원소를 삽입한다.      |
| x = lt.max_size()    | x는 lt가 담을 수 있는 최대 원소의 개수다.(메모리의 크기)     |
| lt.merge(lt2)        | lt2를 lt로 합병 정렬한다.(오름차순 : less)                   |
| lt.merge(lt2,pred)   | lt2를 lt로 합병 정렬한다.pred(조건자)를 기준으로 합병(pred는 이항 조건자) |
| lt.pop_back()        | lt의 마지막 원소를 제거한다.                                 |
| lt.pop_front()       | lt의 첫 원소를 제거한다.                                     |
| lt.push_back(x)      | lt의 끝에 x를 추가한다.                                      |
| lt.push_front(x)     | lt의 앞쪽에 x를 추가한다.                                    |
| p=lt.rbegin()        | p는 lt의 역 순차열의 첫 원소를 가리키는 반복자.(const, 비 const 버전 있음) |
| lt.remove(x)         | x 원소를 모두 제거                                           |
| lt.remove_if(pred)   | pred(단항 조건자)가 '참'인 모든 원소를 제거한다.             |
| p=lt.rend()          | p는 lt의 역 순차열의 끝을 표시하는 반복자.(const, 비 const 버전 있음) |
| lt.rsize()           | lt의 크기를 n으로 변경하고 확장되는 공간의 값을 기본값으로 초기화 |
| lt.rsize(n,x)        | lt의 크기를 n으로 변경하고 확장되는 공간의 값을 x로 초기화   |
| lt.reverse()         | lt 순차열을 뒤집는다.                                        |
| lt.size()            | lt 원소의 개수다.                                            |
| lt.sort()            | lt의 모든 원소를 오름차순(less)으로 정렬한다.                |
| lt.sort(pred)        | lt의 모든 원소를 pred(조건자)를 기준으로 정렬한다.(pred는 이항 조건자) |
| lt.splice(p,lt2)     | p가 가리키는 위치에 lt2의 모든 원소를 잘라 붙인다.           |
| lt.splice(p, lt2,q)  | p가 가리키는 위치에 lt2의 q가 가리키는 원소를 잘라 붙인다.   |
| lt.splice(p,lt2,b,e) | p가 가리키는 위치에 lt2의 순차열 [b,e)을 잘라 붙인다.        |
| lt.swap(lt2)         | lt와 lt2를 swap한다.                                         |
| lt.unique()          | 인접한 원소의 값이 같다면 유일한 원소의 순차열로 만든다.     |
| lt.unique(pred)      | 인접한 원소가 pred(이항 조건자)의 기준에 맞다면 유일한 원소의 순차열로 만든다. |

#### 예제

##### push_back() / push_front()/ 반복자

```c++
void main()
{
    list<int>lt;
    
    lt.push_back(10);
    lt.push_back(20);
    lt.push_back(30);
    lt.push_back(40);
    lt.push_back(50);
    
    list<int>::iterator iter;
    
    for(iter = lt.begin(); iter!=lt.end(); ++iter)
        cout << *iter << '';
    
    cout<<endl;
    
    lt.push_front(100);
    lt.push_front(200);
    
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout<< *iter << '';
    
    cout << endl;
}
```

```
//출력 결과
10 20 30 40 50
200 100 10 20 30 40 50
```

push_back() 으로 10부터 50까지 넣어준후 반복자를 이용하여 첫 원소부터 마지막까지 ++iter로 다음 원소에 접근하여 출력해주어서 10 20 30 40 50 과 같은 결과가 나오고 그 후 push_front 로 앞쪽에 값을 추가하게 되니 100 넣고 다시 앞에 200을 넣어주게 되어 200 100 10 20 30 40 50과 같은 결과가 나온다.

##### insert() / erase()

```c++
void main()
{
    list<int> lt;
    
    lt.push_back(10);
    lt.push_back(20);
    lt.push_back(30);
    lt.push_back(40);
    lt.push_back(50);
    
    list<int>::iterator iter = lt.begin();
    list<int>::iterator iter2;
    ++iter;
    ++iter;
    
    iter = lt.erase(iter);
    
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout << endl;
    
    cout << "iter2 : "<<*iter2<<endl;
    
    iter = iter2;
    iter2 = lt.insert(iter,300);
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout << *iter << '';
    cout<<endl;
    
    cout<<"iter2 : "<<*iter2 << endl;
}
```

```
//출력 결과
10 20 40 50
iter2 : 40
10 20 300 40 50
iter2 : 300
```

erase()는 원소를 제거하는 함수이다. 위의 예제에서 `iter = lt.erase(iter);`  iter이 가리키는 원소를 제거하라는 의미로 iter(30)의 원소를 제거하게 되어 출력 했을 때 10 20 40 50이 출력 되게 된다.그리고 이 함수를 이용하여 원소를 제거하면 iter(예제에서는 iter2) 은 다음 원소를 가리키게 된다. 그래서 40이 출력 되는 것이다.

insert()는 가리키는 위치에 원소를 삽입하는 함수이다. `iter2 = lt.insert(iter,300);` iter2(40)이 가리키는  위치에 300을 삽입하게 된다. 

##### remove()

```c++
void main()
{
    list<int>lt;
    
    lt.push_back(10);
    lt.push_back(20);
    lt.push_back(30);
    lt.push_back(10);
    lt.push_back(40);
    lt.push_back(50);
    lt.push_back(10);
    lt.push_back(10);
    
    list<int>::iterator iter;
    for(iter = lt.begin(); iter!=lt.end(); ++iter)
        cout << *iter << ' ';
    cout << endl;
    
    lt.remove(10);
    for(iter = lt.begin(); iter!= lt.end(); ++iter)
        cout << *iter << ' ';
    cout << endl;
}
```

```
//출력 결과
10 20 30 10 40 50 10 10 
20 30 40 50
```

remove()는 원소를 제거하는 함수이다. 예제에서 `lt.remove(10);`을 통해 10 원소의 노드를 모두 제거해주었고 그 결과 10이 제거 된 20 30 40 50만 출력 되는 것을 볼 수 있다.

##### remove_if()

```c++
bool Predicate(int n)
{
    return 10<=n && n <= 30;
}

void main()
{
    list<int> lt;
    
    lt.push_back(10);
    lt.push_back(20);
    lt.push_back(30);
    lt.push_back(40);
    lt.push_back(50);
    lt.push_back(10);
    
    list<int>::iterator iter;
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout << *iter << ' ';
    cout<<endl;
    
    lt.remove_if(Predicate);
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout << *iter << ' ';
    cout << endl;
}
```

```
//출력 결과
10 20 30 40 50 10
40 50
```

remove_if() 는 단항 조건자가 '참'인 모든 원소를 제거하는 함수이다. 위의 예제에서 `bool Predicate(int n)`가 조건자가 되는 것이다. `lt.remove_if(Predicate);`와 같이 적을 수 있으며 Predicate 함수의 조건이 참인 경우니깐 10 20 30은 제거가 되어 40 50만 남게 되는 것이다.

##### splice()

```c++
void main()
{
	list<int>lt1;
	list<int>lt2;

	lt1.push_back(10);
	lt1.push_back(20);
	lt1.push_back(30);
	lt1.push_back(40);
	lt1.push_back(50);

	lt2.push_back(100);
	lt2.push_back(200);
	lt2.push_back(300);
	lt2.push_back(400);
	lt2.push_back(500);

	list<int>::iterator iter;
	cout << "lt1 : ";
	for (iter = lt1.begin(); iter != lt1.end(); ++iter)
		cout << *iter << ' ';
	cout << endl;

	cout << "lt2 : ";
	for (iter = lt2.begin(); iter != lt2.end(); ++iter)
		cout << *iter << ' ';
	cout << endl << "=============" << endl;

	iter = lt1.begin();
	++iter;
	++iter;

	lt1.splice(iter, lt2);

	cout << "lt1 : ";
	for (iter = lt1.begin(); iter != lt1.end(); ++iter)
		cout << *iter << ' ';
	cout << endl;

	cout << "lt2 : ";
	for (iter = lt2.begin(); iter != lt2.end(); ++iter)
		cout << *iter << ' ';
	cout << endl;

}
```

```
//출력 결과
lt1 : 10 20 30 40 50
lt2 : 100 200 300 400 500
=============
lt1 : 10 20 100 200 300 400 500 30 40 50
lt2 : 
```

splice()는 뜻 그대로 잘라 (두 끝을) 붙이는 함수이다. lt1은 10~50까지 lt2는 100~500까지 push_back 함수를 통해 넣어주었다. 여기서 splice를 사용하고자 한다. `iter = lt1.begin();`를 통해 iter는 첫 원소를 가리키게 되었다. 여기서 ++iter를 두번 해줬으니 30 원소를 가리키게 된다. 여기서 `lt1.splice(iter, lt2);`  splice 함수를 이용해보자 iter가 가리키는 위치(30 원소의 위치)에 lt2의 모든 원소를 잘라 붙인다. 그 결과 10 20 100 200 300 400 500 30 40 50 과 같은 출력 결과를 볼 수 있다.

여기서 알아둘점은 리스트에 splice를 통해 한 쪽 리스트에 붙이게 되면 붙이고 난 후의 옮겨진 리스트는 빈 컨테이너가 된다.

아래와 같은 방식으로도 사용 가능하다.

`lt1.splice(iter1,lt2,iter2);` iter1이 가리키는 위치에 iter2가 가리키는 위치의 it2의 원소를 잘라 붙인다.

`lt1.splice(lt1.end(), lt2, lt2.begin(), lt2.end());`  lt1.end()가 가리키는 위치에 순차열 [lt2.begin(), lt2.end())를 잘라 붙인다.



##### reverse()

```c++
void main()
{
    list<int> lt;
    
    lt.push_back(10);
    lt.push_back(20);
    lt.push_back(30);
    lt.push_back(40);
    lt.push_back(50);
    
    list<int>::iterator iter;
    for(iter = lt.begin(); iter !=lt.end(); ++iter)
        cout << *iter << ' ';
    
    cout<<endl;
    
    lt.reverse();
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout << *iter << ' ';
    
    cout << endl;
    
}
```

```
//출력 결과
10 20 30 40 50
50 40 30 20 10
```

reverse 함수는 순차열을 뒤집는 함수로 출력 결과를 보면 알 수 있듯 `lt.reverse();`를 통해 순차열이 뒤집어져 50부터 출력 되는 것을 볼 수 있다.



##### unique()

```c++
void main()
{
    list <int> lt;
    
    lt.push_back(10);
    lt.push_back(10);
    lt.push_back(20);
    lt.push_back(30);
    lt.push_back(30);
    lt.push_back(30);
    lt.push_back(40);
    lt.push_back(50);
    lt.push_back(10);
    
    list<int>::iterator iter;
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout << *iter << ' ';
    cout << endl;
    
    lt.unique();
    for(iter = lt.begin(); iter!=lt.end(); ++iter)
        cout << *iter << ' ';
    cout << endl;    
}
```

```
//출력 결과
10 10 20 30 30 30 40 50 10
10 20 30 40 50 10
```

unique 함수는 중복 원소를 제거하는 함수이다. 그렇지만 중복 원소 없이 원소는 다 다른 하나만 존재하는가? 그렇지 않을수도 있다. 왜냐하면 서로 '인접한' 원소들을 비교 한 후 같은 것이 있다면 모두 소거하고 한 개만을 남기기 때문이다. 예제에서도 알 수 있듯 인접한 두 원소들을 비교해가며 중복 원소를 제거 되었고 첫 원소와 마지막 원소는 같은 10이다. 중복 되는 숫자이지만 서로 인접해 있지 않아서 서로가 중복인것이 확인이 안되어 남아 있게 된다.

##### sort()

```c++
struct Greater
{
    bool operator () (int left, int right) const
    {
        return left > right;
    }
};

void main()
{
    list<int>lt;
    
    lt.push_back(20);
    lt.push_back(10);
    lt.push_back(50);
    lt.push_back(30);
    lt.push_back(40);
    
    list<int>::iterator iter;
    for(iter = lt.begin(); iter !=lt.end(); ++iter)
        cout << *iter << ' ';
    
    cout << endl;
    
    lt.sort();//오름차순 (less, < 연산)정렬
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout << *iter << ' ';
    cout << endl;
    
    lt.sort(greater<int>());//조건자 greater를 사용하여 내림차순 정렬
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout << *iter << ' ';
    cout << endl;
    
    lt.sort(greater<int>());//조건자 less 사용하여 오름차순 정렬
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout << *iter << ' ';
    cout << endl;
    
    lt.sort(Greater());//사용자 정의 조건자를 사용하여 내림차순 정렬
    for(iter = lt.begin(); iter != lt.end(); ++iter)
        cout << *iter << ' ';
    cout << endl;
}

```

```
//출력 결과
20 10 50 30 40
10 20 30 40 50
50 40 30 20 10
10 20 30 40 50
50 40 30 20 10
```

List는 임의의 접근자를 쓸 수 없기 때문에 STL이 제공하는 sort 알고리즘을 사용할 수 없고 스스로 멤버 함수로 가지고 있고 [퀵 정렬](https://hyunjung-til.netlify.com/#/Data_Structure/Sorting?id=퀵-정렬quick-sort)을 이용한 sort 함수이다.



##### merage()

```c++
void main()
{
    list<int> lt1;
    list<int> lt2;
    
    lt1.push_back(10);
    lt1.push_back(20);
    lt1.push_back(30);
    lt1.push_back(40);
    lt1.push_back(50);
    
    lt2.push_back(25);
    lt2.push_back(35);
    lt2.push_back(60);
    
    list<int>::iterator iter;
    cout<<"lt1: ";
    for(iter = lt1.begin(); iter != lt1.end(); ++iter)
        cout<<*iter<<' ';
    cout<<endl;
    
     cout<<"lt2: ";
    for(iter = lt2.begin(); iter != lt2.end(); ++iter)
        cout<<*iter<<' ';
    cout<<endl<<"==================="<<endl;
    
    lt1.merge(lt2);
    
    cout<<"lt1: ";
    for(iter = lt1.begin(); iter != lt1.end(); ++iter)
        cout<<*iter<<' ';
    cout<<endl;
    
     cout<<"lt2: ";
    for(iter = lt2.begin(); iter != lt2.end(); ++iter)
        cout<<*iter<<' ';
    
}
```

```
//출력 결과
lt1: 10 20 30 40 50
lt2: 25 35 60
===================
lt1: 10 20 25 30 35 40 50 60
lt2 :
```

merge는 [합병 정렬](https://hyunjung-til.netlify.com/#/Data_Structure/Sorting?id=병합-정렬merge-sort)을 하는 함수이다. merge는 함칠 두 list가 서로 정렬된 순서의 기준이 다른 상태에서 merge를 하게 되면 오류가 발생한다. `lt1.merge(lt2);` lt2를 lt1 내부로 합병 정렬 한다. 기준은 default 오름차순이다. 합병 된 리스트(여기에서는 lt2)는 빈 컨테이너가 된다.

`lt1.merge(lt2,greater<int>())`  lt2를 lt1으로 합병 정렬하고 두 list의 정렬 기준이 > 연산인 greater라는 것을 predicate로 지정. 이와 같이 이러한 파라미터로 이항 조건자가 오면 그때는 그 기준으로 정렬한다.







> Reference
>
> - SOULSEEK - STL PPT CHAPTER1
> - About STL : C++ STL 프로그래밍