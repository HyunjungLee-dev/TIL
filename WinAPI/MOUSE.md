# MOUSE

- Key를 체크하는 별도의 메세지 대신 Mouse의 3개의 버튼의 상태에 따른 체크를 한다.
- IParam으로 Mouse의 현재 좌표를 알 수 있다. HIWORD : Y 좌표, LOWORD:X좌표
- WM_MOUSEMOVE로 이동체크 이동할 때마다 메세지가 발생한다.

| 버튼   | 누름           | 놓음         | 더블클릭         |
| ------ | -------------- | ------------ | ---------------- |
| Left   | WM_LBUTTONDOWN | WM_LBUTTONUP | WM_LBUTTONBLCLK  |
| Right  | WM_RBUTTONDOWN | WM_RBUTTONUP | WM_RBUTTONDBLCLK |
| Center | WM_MBUTTONDOWN | WM_MBUTTONUP | WM_MBUTTONDBLCLK |

- 좌클릭을 했을 때 좌표 값을 받아서 그 위치에 원을 그리는 코드

```c++
int x;
int y;

LRESULT CALLBACK WndProc(HWND hWnd, UINT iMessage, WPARAM wParam, LPARAM lParam)
{
	HDC hdc;
	PAINTSTRUCT ps;

	switch (iMessage)
	{
		case WM_LBUTTONDOWN:
			x = LOWORD(lParam);
			y = HIWORD(lParam);
			InvalidateRect(hWnd, NULL, TRUE);
			return 0;
		case WM_PAINT:
			hdc = BeginPaint(hWnd, &ps);
			Ellipse(hdc, x, y, x + 100, y + 100);
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