# WinAPI

## WinAPI란?

####  API

API(Application Programming Interface) 는  응용 프로그램 프로그래밍 인터페이스로 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스(사용자가 기기를 쉽게 동작시키는데 도움을 주는 시스템)를 뜻한다. 

#### WinAPI

WinAPI(Windows API)는 마이크로소프트 윈도 운영 체제들이 사용하는 API이다. 즉 WinAPI는 C/C++ 언어의 문법을 이용하여 Windows 응용 프로그램을 제작하게 해 주는 함수의 집합으로 윈도우에서 제공하는 함수로 윈도우 창을 직접 만들어서 사용하는 것이라고 말할 수 있다.  WinAPI 프로그래밍을 할 때 필요한 헤더는 Windows.h 헤더 파일이다.

## WinAPI의 특징

### Windows OS의 특징과 장점

- 그래픽 기반(GUI)의 운영체제이다.

  GUI는 Graphical User Interface의 약자로 사용자에게  키보드로 입력하는 것(예를들어 DOS)이아닌 마우스로 아이콘이나 메뉴를 선택하는 것과 같이 컴퓨터와의 사용자 인터페이스가 그래픽에 의해 구현하는 것이다.

- 멀티 태스킹이 가능하다.

  여러 작업을 동시에 수행 할 수 있다.

- 메시지 구동 시스템이다.

  응용 프로그램은 입력 장치로부터 입력을 직접 읽을 수 없기 때문에 운영체제가 대신 입력 받아 전달해주는데 이것을 메세지라고 하고 이러한 방식을 메시지 구동 시스템 또는 이벤트 드리븐 시스템이라고 한다.  

- 장치에 독립적이고 일관성이 있다.

  윈도우 OS는 디바이스 드라이버에 의해 주변 장치들을 제어하고 관리하기 때문에 장치가 바뀌면 디바이스 드라이브를 교체하면 되기에 응용 프로그램은 이에 영향 받지 않는다.

- 리소스가 따로 분리되어 있다.

  > 리소스란 말 그대로 윈도에서 여러 작업을 하는 데 필요한 '자원' 을 뜻합니다. 윈도가 활용할 수 있는 핵심 메모리 등의 용량으로 이해하면 됩니다.
  >
  > https://news.joins.com/article/1008333

### WinAPI를 배우는 이유

- Windows OS(운영체제)를 이해하기 위해

  API는 운영체제가 제공하는 함수이기에 운영체제 이해하는 것에 가장 가깝다.

- Class Library의 이해를 위해

   클래스 라이브러리는 API 함수의 기반위에 만들어졌다.

- Library와 Visual tool, Engine들의 사용의 이해를 위해

*알아 볼 내용 메모 : 라이브러리와 프레임워크의 차이를 알아보자 / 비주얼 툴*

### API의 변수 명명

해당 변수의 자료형에 맞게 사용 할 수 있도록 이름만 보고 파악 할 수 있게 만들기 위힌 방법으로 헝가리안 표기법이라고 한다. 하지만 무조건 적으로 사용해야하는 것이 아니며 현재 MS 공식 가이드라인에서 권장하지 않는 방법이지만 API에서는 사용하고 있다.

BYTE,CHAR,WORD,DWORD,LONG,BOOL,NULL : WinAPI에서 아용하는 표현법

주의 사항 : NULL의 경우 VS2017버전부터는 nullstr를 권장하고 있다.

### HANDLE

핸들(HANDLE)이란 여러가지 응용프로그램들과 기능들의 메모리에 번호를 붙여 서로를 구분하기 위해 붙여진 정수 값이다.

- 32비트 정수 값을 가진다.
- 운영체제(OS)에서 발급받은 넘버를 사용하기만 한다.
- 같은 종류의 핸들과는 동일 값을 가지지 않는다.(중복 되지 않는다)
- 멀티 태스킹을 위해 서로를 '구분'하기 위한 표식을 하는 숫자일 뿐 특정한 값을 가지는 것이 아니므로 사용 법에 집중하자.

## Visual Studio Create Project

1. 파일을 누르고 새 프로젝트를 선택한 후 Windows 데스크톱 마법사를 선택하고 이름 작성 후 '확인' 버튼을 눌러준다.
2. Windows 데스크톱 프로젝트에서 Windows 응용 프로그램을 선택하고 빈프로젝트에 체크 후 SDL의 체크는 해제해준다.

참고 https://webnautes.tistory.com/1203

## WinMain

```c++
#include<windows.h> // 윈도우 헤더 파일을 불러온다.
LRESULT CALLBACK WndProc(HWND, UINT, WPARAM, LPARAM); // 메세지를 받아서 처리하는 함수
HINSTANCE g_hInst;//글로벌 인스턴스핸들값 H는 Handle의 줄임
LPCTSTR lpszClass = TEXT("HelloWorld"); //창이름

int APIENTRY WinMain(HINSTANCE hInstance, HINSTANCE hPervlnstance, LPSTR lpszCmdParam, int nCmdShow)
{
	HWND hWnd;
	MSG Message;
	WNDCLASS WndClass;
	g_hInst = hInstance;
	//WndClass는 기본 윈도우환경을 만드는 구조체다. 맴버변수는 밑에와 같다.
	WndClass.cbClsExtra = 0; //예약영역
	WndClass.cbWndExtra = 0; //예약영역 (신경x)
	WndClass.hbrBackground = (HBRUSH)GetStockObject(WHITE_BRUSH);	//배경색
	WndClass.hCursor = LoadCursor(NULL, IDC_ARROW);	//커서
	WndClass.hIcon = LoadIcon(NULL, IDI_APPLICATION);	//아이콘 모양
	WndClass.hInstance = hInstance;//(프로그램 핸들값(번호)등록)
	WndClass.lpfnWndProc = WndProc;	//프로세스 함수 호출
	WndClass.lpszClassName = lpszClass;	//클레스 이름
	WndClass.lpszMenuName = NULL;
	WndClass.style = CS_HREDRAW | CS_VREDRAW;//윈도우의 수직과 수평이 변경 시 다시 그린다.
	RegisterClass(&WndClass);  //만들어진 WidClass를 등록

	hWnd = CreateWindow(lpszClass, lpszClass, WS_OVERLAPPEDWINDOW, CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, NULL, (HMENU)NULL, hInstance, NULL);
	ShowWindow(hWnd, nCmdShow);

	while (GetMessage(&Message, NULL, 0, 0))//사용자에게 메시지를 받아오는 함수(WM_QUIT 메시지 받을 시 종료)
	{
		TranslateMessage(&Message); //  키보드 입력 메시지 처리함수
		DispatchMessage(&Message); //받은 메시지를 WndProc에 전달하는 함수
	}
	return (int)Message.wParam;
}

LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	switch (iMessage)
	{
	case WM_DESTROY:// 윈도우가 파괴되었다는 메세지(연관된 리소스도 파괴) WM_은 윈도우 메세지방식
		PostQuitMessage(0); //GetMessage함수에 WM_QUIT 메시지를 보낸다.
		return 0; //WndProc의 Switch는 break 대신 return 0; 를 쓴다.
	}
	return(DefWindowProc(hWnd, iMessage, wParam, lParam)); // case에 있는 메시지를 제외한 나머지 메시지를 처리한다.
}

```



-  APIENTRY WinMain(HINSTANCE hInstance, HINSTANCE hPervlnstance, LPSTR lpszCmdParam, int nCmdShow)

  - HINSTANCE  hInstance : 프로그램 인스턴스의 핸들
  - HINSTANCE  hPervlnstance : Win32에서 항상 NULL 오래된 구버전과의 호환을 위한 것
  - LPSTR  lpszCmdParam : 명령행으로 입력된 프로그램 인수 값(보통 실행 직후에 열 파일의 경로)
  - int nCmdShow : 윈도우 실행 형태

  

- LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam) : 콜백 함수로 윈도우 프로그래밍은 메세지를 받으면 콜백 함수로 보낸 후 그에 따른 처리를 한다.

  - HWND hWnd : 윈도우 핸들
  - UINT iMessage: Unsigned int메세지
  - WPARAM wParam : 메세지 정보 1
  - LPARAM lParam : 메세지 정보 2

- PostQuitMessage : 메세지 루프를 탈출 시킨다. 0을 넣어서 while 메세지 루프를 탈출 시켜 메인의 return이 실행되 종료 되는 방식.











> Reference
>
> - SOULSEEK - WinAPI PPT CHAPTER1
> - [Wiki](https://ko.wikipedia.org/wiki/윈도우_API)
> - https://popbox.tistory.com/93?category=703655
> - https://genesis8.tistory.com/123
> - https://m.blog.naver.com/winterwolfs/10165473492