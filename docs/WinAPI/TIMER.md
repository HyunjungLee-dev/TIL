# TIMER

키보드나 마우스의 경우 사용자로부터 입력 되어져야 메시지가 발생하게 되는데, 타이머의 경우는 타이머 메시지를 통해서 일정시간마다 반복된 코드를 실행하게 지정할수 있다.  같은 동장을 반복해야하는 경우나 시간에 관련 된 (시간 간격을 두고 어떠한 행동을 해야하는 경우 등) 일을 할 때 이 타이머 메시지를 이용하게 된다.

```c++
LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	HDC hdc;
	PAINTSTRUCT ps;
	SYSTEMTIME st; // 시간을 얻어올때 사용하는 구조체
	static TCHAR sTime[128];

	switch (iMessage)
	{
	case WM_CREATE:
		SetTimer(hWnd, 1, 1000, NULL); // 타이머 생성
		SendMessage(hWnd, WM_TIMER, 1, 0); // 윈도우에 메세지 전달
		return 0;
	case WM_TIMER:
		GetLocalTime(&st);
		wsprintf(sTime, TEXT("지금 시간은 %d:%d:%d입니다."),
			st.wHour, st.wMinute, st.wSecond);
		InvalidateRect(hWnd, NULL, TRUE);
		return 0;
	case WM_PAINT:
		hdc = BeginPaint(hWnd, &ps);
		TextOut(hdc, 100, 100, sTime, lstrlen(sTime));
		EndPaint(hWnd, &ps);
		return 0;
	case WM_DESTROY:
		KillTimer(hWnd, 1); // 타이머 파괴
		PostQuitMessage(0); 
		return 0; 
	}
	return(DefWindowProc(hWnd, iMessage, wParam, lParam));
}

```

## SetTimer와 killTimer

### SetTimer

타이머를 생성해주는 함수

**UINT_PTR SetTimer(HWND hwnd, UINT_PTR nIDEvent, UINT uElapse, TIMERPROC lpTimerFunc)**

- 1번째 인수 : `hwnd` 윈도우 핸들
- 2번째 인수 : `nIDEvent` 타이머 넘버로 타이머를 여러개 만들경우 타이머를 구분하기 위해 사용한다.
- 3번째 인수 : `uElapse` 타이머 메시지를 호출할 간격으로 단위는 밀리세컨드이다. 1000을 넣는 경우는 1초가 된다.
- 4번째 인수 : `lpTimerFunc` 메시지가 발생했을 때 마다 호출될 콜백함수로 NULL일 경우는  WndProc()가 WM_TIMER 메시지를 받는다



```c++
LRESULT CALLBACK WndProc(HWND hwnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	HDC hdc;
	PAINTSTRUCT ps;
	static TCHAR sTime[128];

	switch (iMessage)
	{
	case WM_CREATE:
		SetTimer(hwnd, 1, 50, TimeProc);
		SendMessage(hwnd, WM_TIMER, 1, 0);
		return 0;
	case WM_PAINT:
		hdc = BeginPaint(hwnd, &ps);
		Ellipse(hdc, x, y, x+50, y+50);
		EndPaint(hwnd, &ps);
		return 0;
	case WM_DESTROY:
		KillTimer(hwnd, 1);
		PostQuitMessage(0);
		return 0;
	}
	return(DefWindowProc(hwnd, iMessage, wParam, lParam));
}

void CALLBACK TimeProc(HWND hwnd, UINT uMsg, UINT idEvent, DWORD dwTime)
{
	x++;
	InvalidateRect(hwnd, &myRect, TRUE);
}

```

- `SetTimer(hwnd, 1, 50, TimeProc);` 에서 TimeProc 과 같이 4번째 인수에 CALLBACK 함수를 넣어주면 콜백으로 들어오게 된다.
- 연결된 타이머에서 인자 값을 받기 때문에 CALLBACK 함수의 인자는 신경 쓰지 않아도 된다.
- 타이머 메시지가 올때마다 갱신을 해주는 코드가 필요하다면 CALLBACK에서 하는 것이 더 깔끔하다.

### KillTimer

SetTimer로 생성 된 타이머를 파괴하기 위해 사용되는 함수로 타이머를 생성해주었다면 필수적으로 파괴도 해주어야한다.

**BOOL KillTimer( HWND hWnd, UINT uIDEvent )**

- 1번째 인수 : `hwnd` 윈도우 핸들
- 2번째 인수 : `nIDEvent` 타이머 넘버로 SetTimer에서 만들어주었던 타이머의 넘버를 넣어준다.

## WM_TIMER

SetTimer에 지정한 주기마다 발생하는 메세지로 메세지가 발생하는 간격을 이용해서 주기적인 처리를 명령한다.



## SendMessage

SetTimer에서 지정한 주기마다  WM_TIMER 메시지가 발생하게 되는데 그렇게 되면 최초 실행시 SetTimer가 지정한 주기가 지나지 않았기 때문에  WM_TIMER의 메세지가 발생하지 않는다 그렇게 되면 위의 코드 같은 경우는 텍스트가 1초정도 지나야 나오게 되는 것이다. 이러한 상황을 없애주기 위해서 사용하는 것이  SendMessage 이다. 

**LRESULT SendMessage( HWND hWnd, UINT Msg, WPARAM wParam, LPARAM lParam)**

SendMessage는 조건이나 상황과 상관 없이 해당 메시지를 강제로 발생시킬 때 사용하며 MSG 종류에 따라  wParam, lParam에 들어갈 값이 달라진다.

- 1번째 인수 : `hwnd` 윈도우 핸들
- 2번째 인수 : `Msg` 메시지 큐에 넣을 메시지
- 3번째 인수 : `wParam` 메시지의 추가정보
- 4번째 인수 : `lParam`  메시지의 추가정보



> Reference
>
> - SOULSEEK - WinAPI PPT CHAPTER4
> - https://m.blog.naver.com/gtpark91/220657079463

