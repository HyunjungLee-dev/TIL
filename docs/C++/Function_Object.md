# 함수 객체(Function Object)

- 함수자(Functor)라고 불린다.
- 함수처럼 동작하는 객체를 말한다.
- 매개변수 리스트를 갖는 함수 객체도 만들 수 있다.
- 함수처럼 동작하려면 ()연산자를 정의해야 하기때문에 ()연산자를 오버로딩 해야 한다.

```c++
void Print()
{
	cout << "전역 함수!"<<endl;
}

class Functor
{
 public:
 	void operator()()
 	{
 		cout << "함수 객체!" << endl;
 	}
};

void main()
{
	Functor functor;
	
	Print(); // 전역 함수 호출
	functor(); // 멤버 함수 호출 functor.operator()와 같다
}

```



### 함수 객체의 장점

- 일반 함수보다 속도가 빠르다.
  - 인라인이 가능하여 처리 속도를 개선할 수 있다.
  - 컴파일러에 의해 쉽게 최적화 될 수 있다.
- 함수 객체의 서명이 같더라도 객체 타입이 다르면 서로 전혀 다른 타입으로 인식한다.
- 함수 객체는 인라인 될 수 있고, 컴파일러가 쉽게 최적화 할 수 있다.

> Reference
>
> - STL PPT 프롤로그
> - C++ 기초 플러스 6판

