# MESSAGEBOX

`MessageBox(hWnd, IpText, IpCaption, uType)`

- 팝업 박스로 특정 상황을 알려주고 내부버튼의 상태에 따라 동작을 전달 할 수 있다.
- 1번째 인자: hWnd
- 2번째 인자: 표시 할 문자열
- 3번째 인자 : 메세지 박스의 이름
- 4번째 인자 : 메세지 박스 버튼 옵션

| 값                  | 설명                                          |
| ------------------- | --------------------------------------------- |
| MB_ABORTRETRYIGNORE | Abort, Retry, Ignore 세 개의 버튼을 보여준다. |
| MB_OK               | OK버튼을 보여준다.                            |
| MB_OKCANCEL         | OK, Cancel 버튼을 보여준다.                   |
| MB_RETRYCANCEL      | Retry, Cancel 버튼을 보여준다.                |
| MB_YESNO            | YES, NO 버튼을 보여준다.                      |
| MB_YESNOCANCEL      | YES, NO, CANCEL 버튼을 보여준다.              |



- MB_ABORTRETRYIGNORE

![MB_ABORTRETRYIGNORE](https://user-images.githubusercontent.com/54986748/78789202-c3f15200-79e7-11ea-9c07-6c3bf48e1352.PNG)

- MB_OK

![MB_OK](https://user-images.githubusercontent.com/54986748/78789237-d23f6e00-79e7-11ea-88c7-411c0bd261c4.PNG)

- MB_OKCANCEL

![MB_OKCANCEL](https://user-images.githubusercontent.com/54986748/78789266-dc616c80-79e7-11ea-935c-13fdd6247303.PNG)

- MB_RETRYCANCEL

![MB_RETRYCANCEL](https://user-images.githubusercontent.com/54986748/78789293-e71c0180-79e7-11ea-8263-eb93fa7a59eb.PNG)

- MB_YESNO

![MB_YESNO](https://user-images.githubusercontent.com/54986748/78789314-f26f2d00-79e7-11ea-9a91-7f3490604bcd.PNG)

- MB_YESNOCANCEL

![MB_YESNOCANCEL](https://user-images.githubusercontent.com/54986748/78789353-fdc25880-79e7-11ea-943b-491908d86e26.PNG)

### MessageBox의 버튼 처리

| 값       | 설명                    |
| -------- | ----------------------- |
| IDABORT  | Abort 버튼을 눌렀을 때  |
| IDCANCEL | Cancel 버튼을 눌렀을 때 |
| IDIGNORE | Ignore 버튼을 눌렀을 때 |
| IDNO     | NO 버튼을 눌렀을 때     |
| IDOK     | OK 버튼을 눌렀을 때     |
| IDRETRY  | Retry 버튼을 눌렀을 때  |
| IDYES    | Yes 버튼을 눌렀을 때    |

### 코드

```c++
LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	HDC hdc;
	PAINTSTRUCT ps;

	switch (iMessage)
	{
	case WM_LBUTTONDOWN:
		if (MessageBox(hWnd, TEXT("마우스 좌클릭"), TEXT("MessageBox"), MB_YESNOCANCEL) == IDYES)
		{
			
		}

		return 0;
	case WM_PAINT:
		hdc = BeginPaint(hWnd, &ps);
		
		EndPaint(hWnd, &ps);
		return 0;
	case WM_DESTROY:
		PostQuitMessage(0);
		return 0;
	}
	return(DefWindowProc(hWnd, iMessage, wParam, lParam));
}
```



> Reference
>
> - SOULSEEK - WinAPI PPT CHAPTER3