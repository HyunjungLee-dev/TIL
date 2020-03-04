# 템플릿(template)

- 여러 타입의 함수나 클래스를 쉽게 구현 가능하게 한다. 
- 프로그램의 속도에 영향을 주지 않지만, 컴파일하는 도중에 클래스나 함수를 생성해야 하므로 컴파일이 느려지는 단점은 있다.
- 함수 템플릿과 클래스 템플릿이 있다.

## 함수 템플릿

함수 템플릿은 함수의 일반화 서술이다. 함수 템플릿은 int형이나 double형과 같은 구체적인 데이터형을 포괄할 수 있는 일반형(generic type)으로 함수를 정의한다. 어떤 데이터형을 템플릿에 매개변수로 전달하면, 컴파일러가 그 데이터형에 맞는 함수를 생성한다.

```
//Template <typename type> function - declarator
Template <typename T> T Max(T a, T b)
{
	return a>b ? a:b;
}
```



- 함수 앞에 `template<T>` 키워드를 붙이면 된다.
- 매개 변수도 `<T>`여야 한다.
- 명시적, 암시적 호출 둘 다 알맞은 형태의 함수로 변형 시키기 때문에 구분할 필요 없다.

## 클래스 템플릿

- 클래스를 정의하기 위한 메타 클래스 코드
- 템플릿 매개변수 인자를 통해 클래스에 사용될 타입을 결정할 수 있다.

클래스 템플릿을 정의 하는 문법

```
template<typename type>class 클래스 이름
{
	..........
};

template<typename T>class Stack
{
	..........
};
```

정의한 클래스 템플릿을 사용하는 방법

```
Class name <type> 변수명;

Stack<int> kStack;
```











> Reference
>
> - SOULSEEK STL PPT 프롤로그
> - C++ 기초 플러스 6판

