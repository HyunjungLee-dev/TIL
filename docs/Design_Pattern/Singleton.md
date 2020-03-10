# 싱글턴(Singleton)

## 싱글턴 패턴이란

번역하여 '단일체'라고도 하지만 일반적으로 '싱글톤'이라고 한다. 싱글톤 패턴은 전역 변수를 사용하지 않고 객체를 하나만 생성 하도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 패턴이다. 즉 오직 한개의 클래스 인스턴스만을 갖도록 보장하고, 이에 대한 전역적인 접근점(Accecss point)을 제공한다.

### 활용성

- 클래스의 인스턴스가 오직 하나여야 함을 보장하고 잘 정의된 접근점으로 모든 사용자가 접근할 수 있도록 해야 할 때.
- 유일한 인스턴스가 서브클래싱으로 확장되어야 하며, 사용자는 코드의 수정없이 확장된 서브클래스의 인스턴스를 사용할 수 있어야 할 때

### 구조

<img src="https://user-images.githubusercontent.com/54986748/76313315-0f94db00-6318-11ea-8155-a6eae2e69f50.png" alt="singleton" style="zoom:50%;" />

Singleton : Instance() 연산을 정의하여, 유일한 인스턴스로 접근할 수 있도록 한다. Instance()연산은 클래스 연산이다. 

### 특징

1. 유일하게 존재하는 인스턴스로의 접근을 통제한다.
2. 이름 공간을 좁힌다.
3. 연산 및 표현의 정제를 허용한다.
4. 인스턴스의 개수를 변형하기 자유롭다.
5. 클래스 연산을 사용하는 것보다 훨씬 유연한 방법이다.
6. 다른 패턴들의 구현 방법으로 많이 사용된다.



### 구현 방법

- private 생성자만을 정의해 외부 클래스로부터 인스턴스 생성을 차단한다.
- 싱글톤을 구현하고자 하는 클래스 내부에 멤버 변수로써 private static 객체 변수를 만든다.
- public static 메소드를 통해 외부에서 싱글톤 인스턴스에 접근할 수 있도록 접점을 제공한다.



```c++
class Singleton // 클래스 명
{
	static Singleton * m_hThis; // 인스턴스를 넘겨줄 객체
 public:
    //인스턴스가 생성되어 있지 않다면 생성하고 존재하면 반환한다.
    static Singleton * GetInstance()
    {
        if(m_hThis == NULL)
            m_hThis = new Singleton;
        
        return m_hThis;
    }
}

Singleton();
~Singleton();
};
```





> Reference
>
> - SOULSEEK - Design Pattern PPT CHAPTER1
> - https://gmlwjd9405.github.io/2018/07/06/singleton-pattern.html
> - https://readystory.tistory.com/116