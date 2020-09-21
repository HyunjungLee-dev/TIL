# TCP/IP 소켓 프로그래밍

> 윤성우의 열혈 TCP/IP 소켓 프로그래밍 강의를 보고 작성한 것입니다.

## Chapter 01. 네트워크 프로그래밍과 소켓의 이해

###  01-1.네트워크 프로그래밍과 소켓의 이해

#### 네트워크 프로그래밍이란?

- **소켓**이라는 것을 기반으로 프로그래밍을 하기 때문에 소켓 프로그래밍이라고도 한다.
- 네트워크로 연결된 둘 이상의 컴퓨터 사이에서의 데이터 송수신 프로그램의 작성을 의미한다.

#### 소켓에 대한 간단한 이해

- 네트워크(인터넷)의 연결 도구
- 운영체제에 의해 제공이 되는 **소프트웨어적**인 장치
- 소켓은 프로그래머에게 데이터 송수신에 대한 물리적, 소프트웨어적 세세한 내용을 신경 쓰지 않게 한다.

네트워크 프로그래밍이라는 것은 두 개의 컴퓨터, 보통 호스트라고 표현을 하는데 데이터를 주고 받는 방법을 말한다. 데이터를 주고 받는 방법에 있어서 아무것도 없는 상태에서 이것을 완성하는 것에는 무리가 있다. 그렇기에 운영체제에서 소켓이란 것을 제공한다. 

소켓이라는 것은 표준에 의해서 개발 된 하나의 소프트웨어 모듈로 보면 된다. 소켓은 네트워크(인터넷)상에서 두 개의 소켓이 서로 연결이 가능하고 데이터를 주고 받을 수 있는 하나의 소프트웨어적인 도구이다. 

전력망으로부터 전기를 공급받기 위해 소켓을 꽂는 것과 마찬가지로 컴퓨터와 데이터를 송수신하려면 인터넷이라는 네트워크 망을 연결해야 하는데 이때 프로그래밍에서 '소켓'은 네트워크 망의 연결에 사용되는 도구이다. 즉, 연결이라는 의미가 담겨있어서 '소켓'이라는 표현을 사용한다.

------



#### 전화 받는 소켓의 생성

##### 소켓의 비유와 분류

- TCP 소켓은 전화기에 비유될 수 있다.
  - 전화기를 생각해보면 전화망에 접속을 해서 상대 전화기에 연결을 요청하는데 즉, 전화망에 연결하는 일종의 도구가 되는 것이다.
- 소켓은 soket 함수의 호출을 통해서 생성한다.
  - 소켓을 실제로 생성해서 관리하는 것은 운영체제이고 함수 호출을 통해서 운영체제가 그에 적절한 조치를 소켓을 기반으로 해서 진행한다.
- 단, 전화를 거는 용도의 소켓과 전화를 수신하는 용도의 소켓 생성 방법에는 차이가 있다.

**[소켓의 생성]**

```c
#include <sys/socket.h>
int soket(int domain, int type, int protocol);
//->성공 시 파일 디스크립터, 실패 시 -1 반환
```

#### 전화번호의 부여

##### 소켓의 주소 할당 및 연결

- 전화기에 전화번호가 부여되듯이 소켓에도 주소정보가 할당된다.
- 소켓의 주소정보는 IP와 PORT번호로 구성이 된다.

**[주소의 할당]**

```c
#include <sys/socket.h>
int bind(int sockfd, struct sockaddr *myaddr, socklen_t addrlen);
//-> 성공 시 0, 실패 시 -1 반환
```

#### 전화기의 연결

##### 연결요청이 가능한 상태의 소켓

- 연결요청이 가능한 상태의 소켓은 걸려오는 전화를 받을 수 있는 상태에 비유할 수 있다.
- 전화를 거는 용도의 소켓은 연결요청이 가능한 상태의 소켓이 될 필요가 없다. 이는 걸려오는 전화를 받는 용도의 소켓에서 필요한 상태이다.

**[연결요청 가능한 상태로 변경]**

```c
#include<sys/socket.h>
int listen(int socketfd, int backlog);
// -> 성공 시 0 , 실패시 -1 반환
```

소켓에 할당된 IP와 PORT번호로 연결요청이 가능한 상태가 된다.

#### 수화기를 드는 상황

##### 연결요청의 수락

- 걸려오는 전화에 대해서 수락의 의미로 수화기를 드는 것에 비유할 수 있다.
- 연결요청이 수락되어야 데이터의 송수신이 가능하다.
- 수락된 이후에 데이터의 송수신은 양방향으로 가능하다

**[연결요청 가능한 상태로 변경]**

```c
#include <sys/socket.h>
int accept(int sockfd, struct sockaddr *addr, socklen_t *adrlen);
// 성고 시 파일 디스크립터, 실패 시 -1 반환
```

accept 함수호출 이후에는 데이터의 송수신이 가능하다. 단, 연결요청이 있을 때에만 accept 함수가 반환을 한다.

------

#### 정리

##### 연결요청을 허용하는 소켓의 생성과정

- 1단계. 소켓의 생성(socket 함수호출)
- 2단계. IP와 PORT번호의 할당(bind 함수호출)
- 3단계. 연결요청 가능상태로 변경(listen 함수호출)
- 4단계. 연결요청에 대한 수락(accept 함수호출)

##### 예제 hello_server.c를 통해서 함수의 호출과정 확인하기

- 연결요청을 허용하는 프로그램을 가리켜 일반적으로 서버(Server)라 한다.
- 서버는 연결을 요청하는 클라이언트보다 먼저 실행되어야 한다.
- 클라이언트보다 복잡한 실행의 과정을 거친다.

**이렇게 생성된 소켓을 가리켜 서버 소켓 또는 리스닝 소켓이라 한다.**

------

### 윈도우에서 리눅스 개발 환경 설정(WSL 설치 및 VS Code 연동)

#### 설치

1. Windows 10 607 버전 이상이 필요하며 [제어판]->[프로그램]->프로그램 및 기능 아래에 Windows 기능 켜기/끄기] -> [Linux용 Windows 하위 시스템] 체크 또는 PowerShell을 관리자 권하느로 열고 아래의 명령을 실행한다. 후에 컴퓨터를 재시작 한다.

```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

2. Microsoft Store에서 Ubuntu를 설치한다.
   1.  terminal을 설치한다.(추가적)
3. 설치가 완료 되면 실행을 한다. Ubuntu를 실행하거나 명령 프롬프트에서 wsl을 입력한다. 

#### Visual Studio Code와 WSL 연동

- WSL : 리눅스용 윈도우즈 서브 시스템

1. Visual Studio Code를 windows에 설치한다.
2. Visual Studio Code를 실행하여 Remote Development 확장 프로그램을 추가 설치한다.
3. 윈도우 측의 Git에서 소스코드의 line ending을 윈도우즈 형식으로 변경하지 못하도록 설정한다. 윈도우 프롬프트에서 git config --global core.autocrlf input 명령을 입력한다.

#### WSL의 폴더 열기

WSL 내부의 폴더를 VSCode를 이용하여 여는 방법

1. 시작 메뉴나 명령어 프롬프트에서 wsl을 입력해 WSL 터미널 창을 ㅇㄴ다.
2. 터미널을 열고 열고자 하는 폴더로 이동하여 (cd ~ 명령어를 사용) code .를 입력한다.
3. 진행이 완료된 후, VSCode 창이 나오며 하단에서 WSL 표시를 볼 수 있다.

> 관련 블로그
>
> [YJcode](https://yjcode.tistory.com/1?category=811393)
>
> *위 블로그에서 키 설정 내용은 [dev_(by may)](https://blog.naver.com/PostView.nhn?blogId=rorean&logNo=221346968488&parentCategoryNo=&categoryNo=8&viewDate=&isShowPopularPosts=true&from=search) 확인
>
> [학습기록 (by 쓴웃음)](https://rottk.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-%EC%96%B4%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%EA%B0%9C%EB%B0%9C%EC%9D%84-%EC%9C%84%ED%95%9C-WSL-%EC%84%A4%EC%B9%98-%EB%B0%8F-VS-Code-%EC%97%B0%EB%8F%99)
>
> [sxin2949.lg (by sxin2949)](https://velog.io/@sxin2949/%EC%9C%88%EB%8F%84%EC%9A%B0%EC%97%90%EC%84%9C-%EB%A6%AC%EB%88%85%EC%8A%A4-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0)

------

#### 전화 거는 소켓의 구현

##### 연결을 요청하는 소켓의 구현

- 전화를 거는 상황에 비유할 수 있다.
- 리스닝 소켓과 달리 구현의 과정이 매우 간단하다.
  - 걸려오는 전화를 받는 역할, 리스닝 소켓(=서버 소켓)
- '소켓의 생성'과 '연결의 요청'으로 구분된다.

**[연결의 요청]**

```c
#include <sys/soket.h>
int connect(int sockfd, struct sockaddr *serv_addr, socklen_t addrlen);
// 성공 시 0, 실패 시 -1 반환
```

#### 예제 hello_client.c를 통해서 함수의 호출과정 확인하기

- 함수의 호출과 데이터가 실제 송수신 됨을 확인하자.
- 소스코드의 이해는 점진적으로

 

------

### 01-2. 리눅스 기반 파일 조작하기

#### 저 수준 파일 입출력과 디스크립터

##### 저 수준 파일 입출력

- ANSI의 표준함수가 아닌, **운영체제가 제공하는** 함수 기반의 파일 입출력.
- 표준이 아니기 때문에 운영체제에 대한 호환성이 없다.
- **리눅스는 소켓도 파일**로 간주하기 때문에 저 수준 파일 입출력 함수를 기반으로 소켓 기반의 데이터 송수신이 가능하다.
  -  리눅스가 파일을 처리하는 방법(기준)이 있는데 그 기준에 동일하게 소켓을 처리하기 때문에 파일을 처리하기 위해서 제공한  파일 입출력 함수를 그대로 소켓에 적용해서 데이터를 주고 받는데 사용할 수 있다.

| 파일 디스크립터 |           대 상            |
| :-------------: | :------------------------: |
|        0        | 표준입력 : Standard Input  |
|        1        | 표준출력 : Standard Output |
|        2        | 표준에러 : Standard Error  |

##### 파일 디스크립터

- 운영체제가 만든 파일(그리고 소켓)을 구분하기 위한 일종의 숫자
- 저 수준 파일 입출력을 목적으로 파일 디스크립터를 요구한다.
- 저 수준 파일 입출력 함수에게 소켓의 파일 디스크립터를 전달하면, 소켓을 대상으로 입출력을 진행한다.

------

#### 파일 열기와 닫기 

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <fcnt1. h>

int open(const char *path, int flag);
// 성공 시 파일 디스크립터, 실패 시 -1 반환
```

- path : 파일 이름을 나타내는 문자열의 주소 값 전달
- flag : 파일의 오픈모드 정보 전달

두 번째 매개변수 flag에 전달할 수 있는 값과 의미는 다음과 같으며, 하나 이상의 정보를 비트 OR 연산자로 묶어서 전달이 가능하다.

**[파일의 오픈 모드]**

| 오픈 모드 | 의 미                                  |
| :-------: | -------------------------------------- |
|  O_CREAT  | 필요하면 파일을 생성                   |
|  O_TRUNC  | 기존 데이터 전부 삭제                  |
| O_APPEND  | 기존 데이터 보존하고, 뒤에 이어서 저장 |
| O_RDONLY  | 읽기 전용으로 파일 오픈                |
| O_WRONLY  | 쓰기 전용으로 파일 오픔                |
|  O_RDWR   | 읽기, 쓰기 겸용으로 파일 오픈          |

open 함수 호출 시 반환된 파일 디스크립터를 이용해서 파일 입출력을 진행하게 된다.

```c
#include <unistd.h>

int close(int fd);
//성공시 0, 실패시 -1 반환
```

- fd : 닫고자 하는 파일 또는 소켓의 파일 디스크립터 전달.

위 함수는 파일뿐만 아니라, 소켓을 닫을 때에도 사용된다. 이는 파일과 소켓을 구분하지 않는다는 리눅스 운영체제의 특성 때문이다.

------

#### 파일에 데이터 쓰기

```c
#include <unistd.h>

ssize_t write(int fd, const void * buf, size_t nbytes);
// 성공 시 전달한 바이트 수, 실패 시 -1 반환
```

- fd : 데이터 전송대상을나타내는 파일 디스크립터 전달

- buf : 전송할 데이터가 저장된 버퍼의 주소 값 전달.
- nbytes : 전송할 데이터의 바이트 수 전달.

```c
int main(void)
{
	int fd;
	char buf[]="Let's go!\n";
	fd=open("data.text", O_CREAT|O_WRONLY|O_TRUNC);
	if(fd==-1)
		error_handling("open() error!");
	printf("flie descriptor : %d \n",fd);
	
	if(write(fd,buf,sizeof(buf))==-1)
		error_handling("write() error!");
	close(fd);
	return 0;
}
```

```c
root@my_linux:/tcpip# gcc low_open.c -o lopen
root@my_linux:/tcpip# ./lopen
file descriptor : 3
root@my_linux:/tcpip# cat data.txt
Let's go!
root@my_linux:/tcpip#
```

------

#### 파일에 저장된 데이터 읽기

```c
#include <unistd.h>

ssize_t read(int fd, void *buf, size_t nbyes);
//성공 시 수신한 바이트 수(단 파일의 끝을 만나면 0), 실패 시 -1 반환
```

- fd : 데이터 수신대상을 나타내는 파일 디스크립터 전달
- buf : 수신한 데이터를 저장할 버퍼의 주소 값 전달
- nbytes : 수신할 최대 바이트 수 전달.

```c
int main(void)
{
    int fd;
    char buf[BUF_SIZE];
    
    fd=open("data.txt",O_RDONLY);
    if(fd == -1)
        error handling("open() error!");
    printf("file descriptor : %d \n", fd);
    
    if(read(fd, buf, sizeof(buf))== -1)
        error_handling("read() error!");
    printf("file data: %s", buf);
    close(fd);
    return 0;
}
```

```
root@my_linux:/tcpip# gcc low_read.c -o lread
root@my_linux:/tcpop# ./lread
file descriptor : 3
file data : : Let's go!
root@my_linux:/tcpip#
```

------

#### 파일 디스크립터와 소켓

```c
int main(void)
{
	int fd1, fd2, fd3;
	fd1=socket(PF_INET, SOCK_STREAM, 0);
	fd2=open("test.dat", O_CREAT|O_WRONLY|O_TRUNC);
	fd3=socket(PF_INET, SOCK_DGRAM,0);
	
	printf("flie descriptor 1: %d\n", fd1);
	printf("flie descriptor 2: %d\n", fd2);
	printf("flie descriptor 3: %d\n", fd3);
	close(fd1); close(fd2); close(fd3);
	return 0;
}
```

```
root@my_linux:/tcpip# gcc fd_seri.c -o fds
root@my_linux:/tcpip# ./fds
flie descriptor 1: 3
flie descriptor 2: 4
flie descriptor 3: 5
root@my_linux:/tcpip#
```

실행결과를 통해서 소켓과 파일에 일련의 파일 디스크립터 정수 값이 할당됨을 알 수 있다. 그리고 이를 통해서 리눅스는 파일과 소켓을 동일하게 간주함을 확인할 수 있다. 3부터 시작하는 이유는 0 1 2는 표준 입력,출력,에러에 이미 할당 되어 있기 때문이다.

------

### 01-3. 윈도우 기반으로 구현하기

#### 윈도우 소켓을 위한 헤더와 라이브러리의 설정

##### 윈속 기반의 프로그램 구현을 위한 두 가지 설정

- 헤더 파일 winsock2.h의 포함
- ws2_32.lib 라이브러리의 링크
  - 추가 방법 :프로젝트 속성 (단축키 alt + F7 )->구성속성->링커->입력->추가->종속성

 

------

#### 윈속의 초기화

**[윈속 초기화 함수]**

```c
#include <winsock2.h>

int WSAStartup(WORD wVersionRequested, LPWSADATA lpWSAData);
// 성공 시 0, 실패 시 0이 아닌 에러코드 값 반환
```

- wVersionRequested : 프로그래머가 사용할 윈속의 버전정보 전달
  - MAKEWORD라는 매크로 함수를 이용
- lpWSAData : WSADATA라는 구조체 변수의  주소 값 전달.

**[코드상에서의 초기화 방법]**

```c
int main(int argc, char* argv[])
{
    WSADATA wsaData;
    . . . .
    if(WSAStartup(MAKEWORD(2,2),&wsaData)!= 0)
        ErrorHandling("WSAStartup() error!");
    . . . .
    return 0;
}
```

윈속의 초기화란, 윈속 함수호출을 위한 라이브러리의 메모리 LOAD를 의미한다.

------

#### 윈속 라이브러리의 해제

다음 함수가 호출되면 할당된 윈속 라이브러리는 윈도우 운영체제에 반환이 되면서, 윈속 관련 함수의 호출이 불가능해지므로, 프로그램이 종료되기 직전에 호출하는 것이 일반적이다.

**[윈속 라이브러리를 해제시키는 함수]**

```C
#include <winsock2.h>

int WSACleanup(void);
// 성공 시 0, 실패 시 SOCKET_ERROR 반환
```

------

### 01-4. 윈도우 기반의 소켓관련 함수와 예제

#### 윈도우 기반 소켓관련 함수들 ONE

**[리눅스의 socket 함수에 대응]**

```c
#include <winsock2.h>

SOCKET socket(int af, int type, int protocol);
//성공 시 소켓 핸들, 실패 INVALID_SOCKET 반환
```

**[리눅스의 bind 함수에대응]**

```c
#include <winsock2.h>

int bind(SOCKET s, const struct sockaddr * name, int namelen);
//성공 시 소켓 핸들, 실패 시 INVALID_SOCKET 반환
```

리눅스에서의 파일 디스크립터에 해당하는 것을 윈도우에서는 **핸들(HANDLE)**이라 한다.

**[리눅스 listen 함수에 대응]**

```c
#include <winsock2.h>

int listen(SOCKET s, int backlog);
//성공 시 0, 실패 시 SOCKET_ERROR 반환
```

**[리눅스의 accept 함수에 대응]**

```c
#include <winsock2.h>

SOCKET accept(SOCKET s, struct sockaddr * addr, int * addrlen);
//성공 시 소케 핸들, 실패 시 INVALID_SOCKET 반환
```

**[리눅스의 connect 함수에 대응]**

```c
#include<winsock2.h>

int connect(SOCKET s, const struct sockaddr * name, int namelen);
// 성공 시 0, 실패 시 SOCKET_ERROR 반환
```

**[리눅스의 close 함수에 대응]**

```c
#include <winsock2.h>

int closesocket(SOCKET s);
// 성공 시 0, 실패 시 SOCKET_ERROR 반환
```

리눅스 같은 경우에는 소켓을 파일로 간주하기 때문에 파일 close 하는 함수를 그대로 사용해서 소켓을 종료한다. 그런데 윈도우의 경우는 

소켓과 파일을 구분한다. 그 두 개를 동일시하지 않도록 운영체제가 디자인 되어있다. 그렇기에 별도의 소켓 종료 함수를 제공한다. 

------

#### 윈도우 기반 서버, 클라이언트 예제 실행하기

##### 예제 hello_server_win.c, hello_client_win.c의 실행

**[실행결과 : hello_server_win.c]**

```
c:\tcpip\hServerwin 9190
```

**[실행결과 : hello_client_win.c]**

```
c:\tcpip>hClientWin 127.0.01 9190
Message fron server : Hello World!
```

소스코드를 통해서 다음 두 가지 사실을 관찰하자.

1. 소켓의 생성과정에 따른 함수의 호출
2. 리눅스 기반에서 호출했던 소켓 기반 입출력 함수에 어떠한 차이가 있는가?

------

#### 윈도우 기반 입출력 함수

##### 윈도우에서는 별도의 입출력 함수를 사용

- 리눅스와 달리 파일과 소켓을 별도의 리소스로 구분한다.
- 때문에 파일 입출력 함수와 소켓 기반의 입출력 함수에 차이가 있다.



```c
#include <winsocket2.h>

int send(SOCKET s, const char * buf, int len, int flags);
//성공 시 전송된 바이트 수 , 실패 시 SOCKET_ERROR 반환
```

- s : 데이터 전송 대상과의 연결을 의미하는 소켓의 핸들 값 전달
- buf : 전송할 데이터를 저장하고 있는 버퍼의 주소 값 전달
- len : 전송할 바이트 수 전달
- flags : 데이터 전송시 적용할 다양한 옵션 정보 전달.



```c
#include <winsock2.h>

int recv(SOCKET s, const char * buf, int len, int flags);
// 성공 시 수신한 바이트 수 (단 EOF 전송 시 0), 실패 시 SOCKET_ERROR 반환
```

- s : 데이터 수신 대상과의 연결을 의미하는 소켓의 핸들 값 전달
- buf : 수신된 데이터를 저장할 버퍼의 주소 값 전달.
- len : 수신할 수 있는 최대 바이트 수 전달
- flags : 데이터 수신 시 적용할 다양한 옵션 정보 전달

------

## Chapter 02. 소켓의 타입과 프로토콜의 설정

###  02-1. 소켓의 프로토콜과 그에 따른 데이터 전송 특성

#### 프로토콜의 이해와 소킷의 생성

소켓은 어떠한 한 가지 송수신 방법을 위해서 만들어진 도구가 아니라 다양한 송수신 방법을 지원 할 수 있도록 일반화 되어서 설계된 것이 소켓이다. 따라서 소켓을 생성할 때 어떠한 방식으로 데이터를 송수신 할 것인지 명령해서 내가 원하는 형태의 소켓을 만들 수 있다.

##### 프로토콜이란?

- 개념적으로 **약속**의 의미를 담고 있다.
- 컴퓨터 상호간의 **데이터 송수신에 필요한 통신규약**.
- 소켓을 생성할 때 기본적인 프로토콜을 지정해야 한다.

```c
#include <sys/socket.h>

int socket(int domain, int type, int protocol)
//성공 시 파일 디스크립터, 실패 시 -1 반환
```

- domain 소켓이 사용할 프로토콜 체계(Protocol Family) 정보 전달.
  - 어떤 도구를 쓸 것인가(편지를 예로들면 빠른,일반,등기와 같은)
- type 소켓의 데이터 전송방식에 대한 정보 전달.
  - 하나의 도구 내에서도 타입이 나누어질 수 있다.(등기에서도 여러가지로 나뉘어질 수 있듯이)
- protocol 두 컴퓨터간 통신에 사용되는 프로토콜 정보 전달.

매개변수 domain, type 그리고 protocol이 모두 프로토콜 정보와 관련이 있다.

------

#### 프로토코 체계(Protcol Family)

##### 프로토콜 체계

위에서 domain으로 이야기 하던 것

- 프로토콜도 그 종류에 따라서 부류가 나뉘는데, 그 부류를 가리켜 **프로토콜 체계**라 한다.
- 프로토콜의 체계 PF_INEF은 IPv4 인터넷 프로토콜 체계를 의미한다. 우리는 이를 기반으로 소켓 프로그래밍을 학습한다.

**[대표적인 프로토콜 체계 정보]**

| 이름      | 프로토콜 체계(Protocol Family)      |
| --------- | ----------------------------------- |
| PF_INET   | IPv4 인터넷 프로토콜 체계           |
| PF_INET6  | IPv6 인터넷 프로토콜 체계           |
| PF_LOCAL  | 로컬 통신을 위한 UNIX 프로토콜 체계 |
| PF_PACKET | Low Level 소켓을 위한 프로토콜 체계 |
| PF_IPX    | IPX 노벨 프로토콜 체계              |

------

#### 소켓의 타입(Type)

##### 소켓의 타입

- 데이터 전송방식을 의미함.
  - 큰 그림에서의 데이터 전송방식
- 소켓이 생성될 때 소켓의 타입도 결정되어야 한다.

##### 프로토콜 체계 PF_INET의 대표적인 소켓 타입 둘

PF_INET : IPv4를 의미하는 이름

- 연결 지향형 소켓 타입
- 비 연결 지향형 소켓 타입

------

#### 두 타입의 소켓

##### 연결지향형 소켓(SOCK_STREAM = TCP 소켓)의 데이터 전송특성

- 중간에 데이터 소멸되지 않는다.
- **전송 순서대로** 데이터가 수신된다.
- 데이터의 경계가 존재하지 않는다.
  - 데이터를 보낼때 예를들어 함수를 write를 두번 호출한다 했을때 처음에 호출 할 때는 5바이트를 전송하고 두번째 전송할 때는 10바이트를 전송 했다고 해서 상대방이 read 함수를 호출해서 처음에 5바이트를 읽고 그 다음에 read 함수를 호출해서 10바이트를 읽을 필요가 없다는 것, 한번의 read 함수 호출을 통해 총 15바이트를 한번에 읽어드릴 수 있다는 것.
- 소켓대 소켓의 연결은 **반드시 1대 1**의 구조

##### 비 연결지향형 소켓(SOCK_DGRAM = UDP 소켓)의 데이터 전송 특성

- **전송 순서 상관없이** **빠른 속도**의 전송을 지향
- 데이터 손실 및 파손의 우려가 있다
  - TCP는 손실 및 파손이 났을 경우 인지하고 재요청을 데이터를 재수신한다 . 하지만 UDP 같은경우는 손실 되었다고 해서 상대방이 그것을 인식하지 못한다.
- 데이터의 경계가 존재한다.
  - 예를들어 write 함수를 이용해 3바이트를 전송하고 또 write 함수를 통해 5바이트를 전송했을때 읽어드리는쪽에서는 read 함수 호출을 통해서 3바이트를 읽어드려야 하고  또 한번 read 함수를 호출해 5바이트를 읽어드려야한다.
- 한번에 전송할 수 있는 데이터의 크기가 제한된다.

------

#### 프로토콜의 최종선택

IPv4 인터넷 프롵콜 체계에서 동작하는 연결지향형 데이터 전송 소켓

```c
int tcp_socket=socket(PF_INET, SOCK_STREAM, IPPROTO_TCP) //TCP 소켓
```

IPv4 인터넷 프로토콜 체계에서 동작하는 비 연결지향형 데이터 전송 소켓

```c
int udp_socket=sockt(PF_INET, SOCK_DGRAM, IPPROTO_UDP) //UDP 소켓
```

첫 번째, 두 번째 인자로 전달된 정보를 통해서 소켓의 프로토콜이 사실상 결정되기 때문에 세 번째 인지로 0을 전달해도 된다.

------

#### 연결지향형 소켓, TCP소켓의 예

전송되는 데이터의 경계(boundary)가 존재하지 않음을 확인하자

```c
if(bind(serv_sock, (struct sockaddr*) &serv_addr,sizeof(serv_addr)) == -1)
	error_handling("bind() error");
if(listen(serv_sock,5)== -1)
	error_handling("listen() error");
clnt_addr_size=sizeof(clnt_addr);
clnt_sock=accept(serv_sock, (struct sockaddr*)&clnt_addr, &clnt_addr_size);
if(clnt_sock==-1)
	error_handling("accept() error");
//write(clnt_sock, message, sizeof(message));  <- tcp_server.c 의 데이터 전송
close(clnt_sock),
close(serv_sock);
```

```c
if(connect(sock, (struct sockaddr*)&serv_add, sizeof(serv_addr))==-1)
    error_handling("connect() error!");
/*while(read_len=read(sock, &message[idx++],1)) 
{
    if(read_len==-1)
    {
        error_handling("read() error!");
        break;
    }
    str_len+=read_len;
} tcp_clientc의 데이터 수신*/
printf("Message from server: %s \n", message);
printf("Function read call count : %d \n",str_len);
```

```
실행결과
root@my_linux:/tcpip# gcc tcp_client.c -o hclient
root@my_linux:/tcpip# ./hclient 127.0.0.1 9190
Message from server : Hello World!
Function read call count: 13
```

------

### 02-2. 윈도우 기반에서 이해 및 확인하기

#### 윈도우 운영체제의 socket 함수

```c
#include <winsock2.h>

SOCKET socket(int af, int type, int protocol);
//성공 시 소켓 핸들, 실패 시 INVALID_SOCKET 반환
```

**[윈도우 소켓 생성의 예]**

```c
SOCKET soc=socket(PF_INET, SOCK_STREAM, IPROTO_TCP);
if(soc==INVALID_SOCKET)
	ErrorHandling(". . . ");
```

반환형이 SOCKET인, 이는 정수로 표현되는 소켓의 핸드 값을 저장하기 위해 정의된 자료형의 이름이다. 

오류발생시 반환하는 INVALID_SOCKET도 오류발생을 알리는 하나의 상수이다. 이 값은 -1이지만 if(soc == -1) 과 같이 작성하게 되면 위와 같은 상수를 정의한 의미가 없어지고 MS에서 향후에 INVALID_SOCKET의 값을 변경해도 문제가 발생하지 않는다.

프로토콜은 표준이다. 따라서 소켓의 타입에 따른 데이터의 전송특성은 운영체제와 상관없이 동일하다.

------

## Chapter 03. 주소체계와 데이터 정렬

### 03-1. 소켓에 할당되는 IP주소와 PORT번호

#### 인터넷 주소(Internet Address)

##### 인터넷 주소란?(IP라는 것은)

- 인터넷상에서 **컴퓨터를** 구분하는 목적으로 사용되는 주소
- 4바이트 주소체계인 **IPv4**와 16바이트 주소체계인 **IPv6**가 존재한다.
  - 4byte의 데이터를 가지고 표현할 수 있는 주소의 수는 2^32개
  - IPv4가 고갈되기 전에 만들어진 주소 체계가 IPv6, 만들 수 있는 주소의 수가 2^128개(무한대에 가깝게)
- 소켓을 생성할 때 기본적인 프로토콜을 지정해야 한다.
- **네트워크 주소**와 **호스트 주소**로 나뉜다. 네트워크 주소를 이용해서 네트워크를 찾고, 호스트 주소를 이용해서 호스트를 구분한다.
  - 나누어둔 이유는 IP의 효율적인 관리를 위해서이다.

![캡처](https://user-images.githubusercontent.com/54986748/93660004-aab7fb80-fa85-11ea-9fd3-a14d51043222.PNG)

------

#### 클래스 별 네트워크 주소와 호스트 주소의 경계

- 클래스 A의 첫 번째 바이트 범위  0이상 127이하
- 클래스 B의 첫 번째 바이트 범위 128이상 191이하
- 클래스 C의 첫번째 바이트 범위 192이상 223이하

이는 다음과 같이 달리 표현 할 수도 있다.

- 클래스 A의 첫 번째 비트는 항상 0으로 시작
- 클래스 B의 첫 두 비트는 항상 10으로 시작
- 클래스 C의 첫 세비트는 항상 110으로 시작

이러한 기준이 정해져 있기 때문에 첫 번째 바이트 정보만 참조해도 IP주소의 클래스 구분이 가능하며, 이로 인해서 네트워크 주소와 호스트 주소의 경계 구분이 가능하다.

------

#### 소켓의 구분에 활용되는 PORT 번호

##### PORT번호

- IP는 컴퓨터를 구분하는 용도로 사용되며, PORT 번호는 **소켓을 구분하는 용도**로 사용된다.
- 하나의 프로그램 내에선 둘 이상의 소켓이 존재할 수 있으므로, 둘 이상의 PORT가 하나의 프로그램에 의해 할당될 수 있다.
- PORT번호는 16비트로 표현, 따라서 그 값은 0 이상 65535 이하
- 0~1023은 잘 알려진 PORT(Well-known PORT)라 해서 이미 용도가 결정되어 있다.

![캡처2](https://user-images.githubusercontent.com/54986748/93660088-7bee5500-fa86-11ea-92ae-0c9caae52a59.PNG)

------

### 03-2 주소정보의 표현

#### IPv4 기반의 주소표현을 위한 구조체

```c
struct sockaddr_in
{
	sa_family_t		sin_family; //주소체계
	uint16_t		sin_port;  //PORT번호
	struct in_addr	sin_addr;  //32비트 IP주소
	char			sin_zero[8]; //사용되지 않음
	
}
```

```c
struct in_addr
{
	in_addr_t		s_add; //32비트 IPv4 인터넷 주소
}
```

IP주소와 PORT번호 구조체 sockaddr_in의 변수에 담아서 표현한다.

**[POSIX에서 정의하고 있는 자료형]**

[^POSIX]: Portable Opearting System Interface, 유닉스 계열의 운영체제에 적용하기 위한 표준

| 자료형 이름 |           자료형에 담길 정보           |
| :---------: | :------------------------------------: |
|   int8_t    |            signed 8-bit int            |
|   uint8_t   |   unsigned 8-bit int (unsigned char)   |
|   int16_t   |           signed 16-bit int            |
|  uinit16_t  |  unsigned 16-bit int(unsigned short)   |
|   int32_t   |           signed 32-bit int            |
|  uint32_t   |  unsigned 32-bit int (unsigned logn)   |
| sa_faily_t  |        주소체계(address family)        |
|  socklen_t  |       길이정보(length of struct)       |
| int_addr_t  |  IP주소정보, uint32_t로 정의되어 있음  |
| int_port_t  | PORT번호정보, uint16_t로 정의되어 있음 |

------

#### 구조체 sockaddr_in의 멤버에 대한 분석

##### 멤버 sin_family

- 주소체계 정보 저장

##### 멤버 sin_port

- 16비트 PORT번호 저장
- 네트워크 바이트 순서로 저장

##### 멤버 sin_addr

- 32비트 IP주소정보 저장
- 네트워크 바이트 순서로 저장
- 멤버 sin_addr의 구조체 자료형 in_addr 사실상 32비트 정수자료형

##### 멤버 siz_zero

0으로 채워야 하는 멤버 sin_zero의 존재 이유를 이해할 필요가 있다.

- 특별한 의미를 지니지 않는 멤버
- 반드시 0으로 체워야 한다.
- 구조체 sockaddr을 IPv4 포맷에 맞게 바이트열을 셋팅하기 위해 정의 된 구조체

**[주소체계]**

| 주소체계(Address Family) | 의 미                                       |
| ------------------------ | ------------------------------------------- |
| AF_INET                  | IPv4 인터넷 프로토콜에 적용하는 주소체계    |
| AF_INET6                 | IPv6 인터넷 프로토콜에 적용하는 주소체계    |
| AF_LOCAL                 | 로컬 통신을 위한 유닉스 프로토콜의 주소체계 |

------

#### 구조체 aockaddr_in의 활용의 예

```
struct sockaddr_in serv_addr;
. . . .
if(bind(serv_sock,(struct sockaddr*)&serv_addr, sizeof(serv_addr)) == -1)
	error_handling("bind() error");
. . . .
```

구조체 변수 sockaddr_in은 bind 함수의 인자로 전달되는데, 매개변수 형이 sockaddr이므로 형 변환을 해야만 한다.

```c
struct sockaddr
{
	sa_maily_t	sin_family; //주소체계(Address Family)
	char		sa_data[14]; //주소정보
}
```

구조체 sockaddr은 다양한 주소체계의 주소정보를 담을 수 있도록 정의되었다. 그래서 IPv4의 주소정보를 담기가 불편하다. 이에 동한 바이트 열을 구성하는 구조체 sockaddr_in이 정의되었으며, 이를 이용해서 쉽게 IPv4의 주소정보를 담을 수 있다.

------

### 03-3 네트워크 바이트 순서와 인터넷 주소 변환

#### CPU에 따라 달라지는 정수의 표현

![image](https://user-images.githubusercontent.com/54986748/93746161-a3345600-fc2f-11ea-9cf8-ac38a2422f58.png)

CPU에 따라서 상위 바이트를 하위 메모리 주세요 저장하기도 하고, 상위 바이트를 상위 메모리 주소에 저장하기도 한다. 즉, CPU마다 데이터를 표현 및 해석하는 방식이 다르다.

------

#### 바이트 순서(Order)와 네트워크 바이트 순서

##### 빅 엔디안(Big Endian)

- 상위 바이트의 값을 작은 번지수에 저장

##### 리틀 엔디안(Little Endian)

- 상위 바이트의 값을 큰 번지수에 저장

##### 호스트 바이트 순서

- CPU별 데이터 저장방식을 의미함

##### 네트워크 바이트 순서

- 통일된 데이터 송수신 기준을 의미함
- 빅 엔디안이 기준이다.

![캡처](https://user-images.githubusercontent.com/54986748/93746466-1b9b1700-fc30-11ea-85b1-c2ffd265ee8e.PNG)

------

#### 바이트 순서의 변환

**[바이트 변환 함수]**

```
unsigned short htons(unsigned short);
unsigned short ntohs(unsigned short);
unsigned long htonl(unsigned long);
unsigned long ntohl(unsigned long);
```

아래의 기준을 적용하면 위 함수가 의미하는 바를 이해할 수 있다.

- htons에서 h는 호스트(host) 바이트 순서를 의미
- htons에서 n은 네트워크(network) 바이트 순서를 의미
- htons에서 s는 자료형 short를 의미
- htonl에서 l은 자료형 long을 의미

------

#### 바이트 변환의 예

```c
int main(int argc, char *argv[])
{
	unsigned short host_port=0x1234;
	unsigned short net_port;
	unsigned long host_addr=0x12345678;
	unsigned long net_addr;
	
	net_port=htons(host_port);
	net_addr=htonl(host_addr);
	
	printf("Host ordered port: %#x \n", host_port);
	printf("Network ordered port: %#x \n", net_port);
	printf("Host ordered address: %x#lx \n", host_addr);
	printf("Network ordered address: %#lx \n", net_addr);
	return 0;
}
```

**[실행 결과]**

```
root@my_linux:/tcpip# gcc endian_conv.c -o conv
root@my_linux:/tcpip# ./conv
Host ordered port: 0x1234
Network ordered port: 0x3412
Host ordered address: 0x12345678
Network ordered address: 0x78563412
```

------

