# DC(Device Context)

## DC란?

먼저 윈도우는 크게 세 가지 동적 라이브러리(DLL, Dynamic Link Library)로 구성 되어 있으며 API 함수들의 대부분은 이 세 가지 DLL에 의해 제공된다.

- 메모리를 관리하고 프로그램을 실행 하는 KERNEL
- 유저 인터페이스와 윈도우를 관리 하는 USER
- 화면 처리와 그래픽을 담담 하는 GDI(Graphic Device Interface)

이때 DC란 Device Context의 약자로 디바이스 컨텍스트, 장치 컨텍스트라고 하며 디스플레이 또는 프린터와 같은 장치의 그리기 특성에 대한 정보를 포함 하는 즉 출력에 필요한 모든 정보를 가지는 Windows 데이터 구조체이며 GDI 모듈에 의해 관리된다. 출력에 사용되는 최소한의 정보만 제공하면 나머지는 DC에 의해 정해진 동작을 하며 해당 윈도우의 핸들을 이용한 타겟 윈도우를 지정해준다. 

## GetDC

```c++
LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	HDC hdc;
	switch (iMessage)
	{
	case WM_DESTROY:
		PostQuitMessage(0);
		return 0;
	case WM_LBUTTONDOWN:
		hdc = GetDC(hWnd);
		TextOut(hdc, 100, 100, TEXT("Beautiful Korea"), 15);
		ReleaseDC(hWnd, hdc);
		return 0;
	}
	return(DefWindowProc(hWnd, iMessage, wParam, lParam));

} // 마우스 좌클릭을 하였을때 Beautiful Korea 메시지가 출력된다.
```

### GetDC()

- Window 핸들 값을 받어서 적당한 DC를 얻어온 후 반환한다.
- 어떤 메세지에서도 모두 사용 가능하며, Window의 상태가 바뀌어서 변화된 정보는 DC에 출력하여 적용시켜주지 않는다. (윈도우 창의 크기가 변경 되거나 다른 윈도우가 겹쳐지면 출력 되지 않는다)
- 한번 받아온 DC는 사용 개수에 제한이 있기 때문에 GetDC 함수를 반복해서 사용하면 DC를  더 이상 사용할 수 없기에 해제해주어야 하는데 GetDC는 ReleaseDC()로 해제해줘야한다.

### TextOut()

- 화면에서 해당 문자열을 출력시키는 함수
- DC의 핸들과 좌표 값과 출력문자열의 정보만으로 문자열을 출력할 수 있다.

### WM_LBUTTONDOWN

- 마으수 좌클릭을 했을 때 호출 되는 메시지.



## WM_PAINT

```c++
LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	HDC hdc;
	PAINTSTRUCT ps;

	switch (iMessage)
	{
	case WM_DESTROY:
		PostQuitMessage(0);
		return 0;
	case WM_PAINT:
		hdc = BeginPaint(hWnd, &ps);
		TextOut(hdc, 100, 100, TEXT("Beautiful Korea"), 15);
		EndPaint(hWnd, &ps);
		return 0;
	}
	return(DefWindowProc(hWnd, iMessage, wParam, lParam));

}
```

### PAINTSTRUCT

- 그리기 전용 구조체로 BeginPaint에 사용한다.



### BeginPaint()

- 윈도우 핸들값과 그리기 전용 구조체를 받아서 그리기용 DC를 생성한 후 반환한다.
- WM_PAINT라는 메시지에서만 사용이 가능하며 창의 정보가 계속 변하여도 그린 부분이 복원될 필요성을 알려줘서 다시 그린다.
- 받아서 사용한 DC는  EndPaint()함수로 해제해줘야한다.



## 문자열 출력

```c++
case WM_PAINT:
		hdc = BeginPaint(hWnd, &ps);
		SetTextAlign(hdc, TA_CENTER);
		TextOut(hdc, 100, 100, TEXT("Beautiful Korea"), 15);
		EndPaint(hWnd, &ps);
		return 0;
```

### SetTextAlign(HDC,UINT)

- TEXT출력 중심점을 설정한다.
- 기본 설정은 TA_TOP|TA_LEFT
  - 여기서 |은 비트 연산자로 OR연산을 한다. [구름EDU](https://edu.goorm.io/learn/lecture/201/한-눈에-끝내는-c언어-기초/lesson/397667/비트-연산자) 참고

|      값       | 설명                                                         |
| :-----------: | ------------------------------------------------------------ |
|    TA_TOP     | 지정된 좌표가 상단이 중심인 좌표가 된다                      |
|   TA_BOTTOM   | 지정된 좌표가 하단이 중심인 좌표가 된다.                     |
|   TA_CENTER   | 지정된 좌표가 수평중앙이 중심인 좌표가 된다.                 |
|   TA_RIGHT    | 지정된 좌표가 수평 오른쪽이 중심인 좌표가 된다.              |
|    TA_LEFT    | 지정된 좌표가 수평 왼쪽이 중심인 좌표가 된다.                |
|  TA_UPDATECP  | 지정된 좌표 대신 CP를 사용하여 문자 출력 후 CP를 변경한다.   |
| TA_NOUPDATECP | CP를 사용하지 않고 지정한 좌표로 출력하며 CP를 변경하지 않는다 |

### RECT

```c++
LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	HDC hdc;
	PAINTSTRUCT ps;
	RECT rt = { 100,100,400,300 };
	TCHAR str[] = TEXT("So keep your eyes on me now"
		"무엇을 보든 좋아할 거야 닿을 수 없는 Level"
		"나와 대결 원한 널 확신해");

	switch (iMessage) {
	case WM_DESTROY:
		PostQuitMessage(0);
		return 0;
	case WM_PAINT:
		hdc = BeginPaint(hWnd, &ps);
		DrawText(hdc, str, -1, &rt, DT_CENTER | DT_WORDBREAK);
		EndPaint(hWnd, &ps);
		return 0;
	}
	return(DefWindowProc(hWnd, iMessage, wParam, lParam));
}
```

4개의 숫자를 기준으로 시작 좌표 x,y에서 뒤에 두 숫자의 크기만큼을 가지는 사각형 범위를 말한다.

<img src="https://user-images.githubusercontent.com/54986748/78361248-0c2d0080-75f3-11ea-8a96-b4f457590d0f.png" alt="rect" style="zoom:50%;" />

|      값       | 설명                                                        |
| :-----------: | ----------------------------------------------------------- |
|    DT_LEFT    | 수평 왼쪽 정렬한다.                                         |
|   DT_RIGHT    | 수평 오른쪽 정렬한다.                                       |
|   DT_CENTER   | 수형 중앙 정렬한다.                                         |
|   DT_BOTTOM   | 사각영역의 바닥에 문자열을 출력한다.                        |
|  DT_VCENTER   | 사각영역의 수직 중앙에 문자열을 출력한다.                   |
| DT_WORDBREAK  | 사각영역의 오른쪽 끝에서 자동 개행 되도록 한다.             |
| DT_SINGLELINE | 한 줄로 출력한다.                                           |
|   DT_NOCLIP   | 사각영역의 경계를 벗어나도 문자열을 자르지 않고 그대로 출력 |

### DrawText

사각형을 그린 뒤 해당 사각형 내부에서 문자를 출력한다.

- 첫 번째 인자 : DC 핸들
- 두 번째 인자 : 출력 문자열
- 세 번째 인자 : 문자열 길이 NULL 문자열이면 -1
- 네 번째 인자 : Left, right, top, bottom 값을 가지는 Rect 구조체를 받아 해당 사각형 영역 안에서 Text 출력 NULL을 받을 시 전체 영역을 다시 그린다.
- 다섯번째 인자 : Draw Text 함수 옵션 설정.

![rect2](https://user-images.githubusercontent.com/54986748/78363200-4ea40c80-75f6-11ea-9a0a-57e1a4025f3a.png)

## 점, 선, 도형 출력

```c++
LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	HDC hdc;
	PAINTSTRUCT ps;


	switch (iMessage) {
	case WM_DESTROY:
		PostQuitMessage(0);
		return 0;
	case WM_PAINT:
		hdc = BeginPaint(hWnd, &ps);
		for (int i = 0; i < 100; i++)
			SetPixel(hdc, 10 + (i * 3), 10, RGB(255, 0, 0));

		MoveToEx(hdc, 50, 50, NULL);
		LineTo(hdc, 300, 90);
		Rectangle(hdc, 50, 100, 200, 180);
		Ellipse(hdc, 220, 100, 400, 200);
		EndPaint(hWnd, &ps);
		return 0;
	}
	return(DefWindowProc(hWnd, iMessage, wParam, lParam));
}
```

![figure](https://user-images.githubusercontent.com/54986748/78364912-3c779d80-75f9-11ea-9dd1-726b9cd7aeb5.png)



### SetPixel()

- 해당 위치에 점을 찍는다.
- 첫 번째 인자 : DC 핸들
- 두 번째, 세 번째 인자 : x,y 좌표값
- 네 번째 인자 : RGB(레드,그린,블루) - 0~255의 넘버

#### SetPixel()로 원 그리기

```c++
void MyCircle(HDC hdc, int x, int y, int r)  
{
	double pi = 3.141592;

	for (int i = 0; i < 360; i++)
	{
		SetPixel(hdc, x + int(sin(i*pi / 180)*r), y + int(cos(i*pi / 180)*r), RGB(0, 255, 0));
	}
}

void MyEllipse(HDC hdc, int x, int y, int rx, int ry) 
{
	double pi = 3.141592;

	for (int i = 0; i < 360; i++)
	{
		SetPixel(hdc, x + int(sin(i*pi / 180)*rx), y + int(cos(i*pi / 180)*ry), RGB(255, 0, 0));
	}
}
```

여기서 봐야하는 부분은 x,y 좌표값이 들어가는 부분이다. 0도부터 360도까지 돌면서 각도 값을 라디안 값으로 변환 후 cos()과 sin() 함수에 넣어서 원을 그려주는 것이다.

그렇다면 라디안(Radian)이란 무엇일까? 각도를 표현하는 단위로는 호도각(Degree)와 라디안(Radian)이 있다. 호도각은 각도를 0도에서 360도까지 표현하는 방법이고 라디안은 반지름이 1인 원에서 호의 길이가 1인 부채꼴의 각을 기본 단위로 삼아 원의 한 바퀴를 2π로 표현하는 방식의 각도 표현법이다. π는 180도를 의미한다. 즉 1도는 π /180 라디안과 같은 값이다.

호도각을 라디안으로 변환 하려면 `radian = degree * Math.PI / 180`

ex. 120° 를 라디안으로 변환 하려면

 	120 x π/180 

​	 120 x π/180 = 120π/180 

​	120 x π/180 = 120π/180 ÷ 60/60 = 2/3π radians

​	120° = 2/3π radians

​	[WikiHow 각로를 라디안 값으로 바꾸는 법](https://ko.wikihow.com/각도를-라디안-값으로-바꾸는-법)

라디안을 호도각으로 변환 하려면 `degree = radian * 180 / Math.PI`

그렇다면 삼각함수를 이용해 어떻게 원을 그릴 수있을까? 

![Tf](https://user-images.githubusercontent.com/54986748/78503525-193c2200-77a2-11ea-9244-1dfcd9bfcfc6.png)

반지름의 길이가 1인 원이 있을 때, 원을 구성하는 각각의 점들의 위치 값을 삼각함수를 이용하여 표현 할 수 있다.  `cos θ = x, sin θ = y` 라고 표현 할 수 있다. 즉 x는 cos θ , y는 sin θ로 θ에 0부터 360까지의 각도를 대입하면 단위 원이 그려지는 것이다.

위의 코드의 경우

![Tf2](https://user-images.githubusercontent.com/54986748/78504951-198ceb00-77ab-11ea-8175-eb4beb605d1e.png)

참조 블로그 

- https://bckong.tistory.com/32 [어느 게임 개발자의 일상]

- [수학벙커](https://m.blog.naver.com/PostView.nhn?blogId=alwaysneoi&logNo=100190371892&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
- https://blog.naver.com/since860321/130166450214





------

![MoveToExLineTo](https://user-images.githubusercontent.com/54986748/78502054-fd348280-7799-11ea-9deb-6591eefdf4b7.png)

### MoveToEx()

- 선의 시작시점을 설정한다.
- 첫 번째 인자 : DC 핸들 값
- 두 번째, 세 번째 인자 : x,y 좌표값
- 네 번째 인자 : 선 이전 좌표 값(통상 NULL)

### LineTo()

- 선의 종료 지점을 설정한다.
- 첫 번째 인자 : DC 핸들 값
- 두 번째, 세 번째 인자 : x,y 좌표값

------



![Rectangle](https://user-images.githubusercontent.com/54986748/78364832-1c47de80-75f9-11ea-8cea-62e611b114fb.png)

### Rectangle()

- 사각형을 그리는 함수
- 첫 번째 인자 : DC 핸들 값
- 2,3,4,5번째 인자 : left, top, right, bottom\

------



![Ellipse](https://user-images.githubusercontent.com/54986748/78364877-308bdb80-75f9-11ea-8c80-c8707cb4e943.png)

### Ellipse()

- 사각형 범위를 잡은 뒤 원형을 그리는 함수
- 첫 번째 인자 : DC 핸들 값
- 2,3,4,5번째 인자 : left, top, right, bottom











> Reference
>
> - SOULSEEK - WinAPI PPT CHAPTER2
> - [ryumin13.tistory](https://ryumin13.tistory.com/entry/DC-Device-Context-란)
> - [diehard98.tistory](https://diehard98.tistory.com/entry/Device-Context의-개념-GetDC-ReleaseDC)
> - https://blog.naver.com/tipsware/220987761947

