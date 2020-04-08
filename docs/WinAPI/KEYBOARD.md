# KEYBOARD

## WM_CHAR

- 키보드 입력이 발생했을 경우 보내는 메세지
- 키보드에서 입력된 문자 키에만 반응한다.
- WM_PAINT에서 따로 그려주는 명령을 수행해야 표현이 가능하다.
- wParam으로 입력 값을 알려준다.

```c++
TCHAR str[256];

LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	HDC hdc;
	PAINTSTRUCT ps;
	int len;

	switch (iMessage)
	{
		case WM_CHAR:
			len = lstrlen(str);
			str[len] = (TCHAR)wParam;
			str[len + 1] = 0;
			InvalidateRect(hWnd, NULL, TRUE);
			return 0;
		case WM_PAINT:
			hdc = BeginPaint(hWnd, &ps);
			TextOut(hdc, 100, 100, str, lstrlen(str));
			EndPaint(hWnd, &ps);
			return 0;
		case WM_DESTROY:
			PostQuitMessage(0);
			return 0;
	}
	return(DefWindowProc(hWnd, iMessage, wParam, lParam));
}
```

위의 코드에서 str[len+1] = 0; 에서 len+1에 0을 넣어주는 이유는 문자열의 끝을 표시하기 위해서이다. 

### lstrlen

int  lstrlen(LPCTSTR ipString) 이 원형으로 ipStirng에는 길이를 조사할 대상 문자열이 들어간며 조사된 길이를 리턴하게 된다.  TextOut 함수의 마지막 인수는 출력할 문자열의 길이를 요구하는데 lstlen 함수로 가능하다.

## InvalidateRect

이것에 대해 알기전에 먼저 무효 영역이라는 것을 알아야한다. 무효영역이란 윈도우 화면의 일부가 변경되어 다시 그려져야 할 부분을 말한다. 윈도우 전체가 다 변경이 되는 경우라면 무효영역과 작업영역을은 동일하다. 

윈도우가 다시 그려져야 하는 상황

1. 윈도우가 처음 생성되었을 때
2. 윈도우의 위치가 이동 되었을 때
3. 윈도우의 크기가 변경 되었을 때, 최대, 최소화 되었을 때
4. 다른 윈도우에 가려져 있다가 드러날 때, 즉 언커버될 때
5. 스크롤 될 때

윈도우에 무효영역이 발생 하면 OS OS는 WM_PAINT 메세지를 발생 시키고 WM_PAINT 메세지 함수 내부의 BeginPaint 함수가 호출 되면서 무효 영역을 유효 영역으로 바꾸어주게 된다.

마찬가지로 프로그램의 내부에서 윈도우의 모습을 변경 시켰을 때는 변경된 부분이 다시 그려질 수 있도록 강제 무효화 시켜주어야 하는데 그때 사용하는 함수가 InvalidateRect이다.

BOOL InvalidateRect(HWND hWnd, const RECT, *IpRect, BOOL bErase);

- 1번째 인수 : hWnd
- 2번째 인수 : 다시 그릴 Rect의 크기 NULL 일 경우 윈도우 전체를 다시 그린다.
- 3번째 인수 : 지정된 범위에 대한 처리를 한다. TRUE일 경우 지우고 다시 그리며 FALSE일 경우 지우지 않고 그린다.

## WM_KEDOWN

- 키보드가 입력되면 전달되는 메세지
- 입력된 모든 키의 정보를 알 수 있다.
- OS에서 설정한 가상 키코드의 값을 알려주며 키보드 종류와 상관없이 범용적인 값을 가진다.
- 영문일 경우 일반 문자열은 대문자와 비교할 수 있다. (ex. if(wParam == 'Z'))

| 가상 키 코드 | 갑(16진수) | 키             |
| ------------ | ---------- | -------------- |
| VK_LEFT      | 0X25       | 좌측 커서 키   |
| VK_RIGHT     | 0X27       | 우측 커서 키   |
| VK_UP        | 0X26       | 위쪽 커서 키   |
| VK_DOWN      | 0X28       | 아래쪽 커서 키 |
| VK_SPACE     | 0X20       | Space          |
| VK_ESCAPE    | 0X1B       | Esc            |
| VK_RETURN    | 0X0D       | Enter          |

```c++
int x = 100;
int y = 100;

LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	HDC hdc;
	PAINTSTRUCT ps;
	int len;

	switch (iMessage)
	{
		
		case WM_PAINT:
			hdc = BeginPaint(hWnd, &ps);
			TextOut(hdc, x, y, TEXT("A"), 1);
			EndPaint(hWnd, &ps);
			return 0;

		case WM_KEYDOWN:

			switch (wParam)
			{
				case VK_LEFT:
					x -= 10;
					break;
				case VK_RIGHT:
					x += 10;
					break;
				case VK_UP:
					y -= 10;
					break;
				case VK_DOWN:
					y += 10;
					break;
			}

			InvalidateRect(hWnd, NULL, TRUE);
		return 0;
		
		case WM_DESTROY:
			PostQuitMessage(0);
			return 0;
	}
	return(DefWindowProc(hWnd, iMessage, wParam, lParam));
}
```

키 코드로 메세지를 받아서 좌표 값을 설정 한 후 다시 지웠다 그리는 것을 이용해 이동하는 것처럼 보이게 된다. 이때 x,y 좌표가 100으로 초기화 되어있는데 이건 콜백 함수에 넣으면 안된다. 매번 초기화 되기때문에 좌표 값이 변하지 않는다.



> Reference
>
> - SOULSEEK - WinAPI PPT CHAPTER3
> - http://printf.egloos.com/551485
> - https://m.blog.naver.com/kater102/122102942

