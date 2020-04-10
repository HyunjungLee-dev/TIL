# MESSAGE

## WINDOW 생성과 파괴

### WM_CREATE

- 윈도우가 생성되면서 받게 되는 메시지
- 윈도우가 생성 되어서 보이기 전에 초기화가 필요하다면 이용할 수 있다.

### WM_DESTROY

- 윈도우가 종료될 때 받게 되는 메시지
- 릴리즈가 필요하다면 이용할 수 있다.

```c++
Switch(iMessage)
{
    case WM_CREATE:
    	mem = (TCHAR*)malloc(1048576);
    retrun 0;
    case WM_DESTROY:
    	free(mem);
    return0;
}
```

위의 코드와 같이 시스템이 정의한 메세지 외에 자신이 필요에 의해 사용 된 것은 WM_DESTROY에서 해제 해 줄 필요가 있다.

Winmain에서 직접 초기화와 종료 처리를 해주는 것도 가능하며 WM_CREATE 메세지 같은 경우는 CreateWindow 함수에 의해 메인 윈도우가 생성 된 직후 보내지므로 CreateWindow 함수 호출문 뒤에 초기화 코드를 직접 작성해주어도 된다.WM_DESTROY 또한 메세지 루프 다음에 종료 처리 코드를 작성해주어도 같은 기능을 한다.



> Reference
>
> - SOULSEEK - WinAPI PPT CHAPTER4
> - http://www.soen.kr/

