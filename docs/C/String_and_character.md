## EOF 에 대하여 

EOF는 파일의 끝을 표현하기 위한 함수이며 -1의 값을 가진다. C에서는 EOF 를 이용해 반복문의 탈출하게 되고 C++에서는 cin.eof()를 이용한다. cin.eof()는 bool 타입을 가지며 EOF를 읽게 되면 true를 반환한다. 

https://lollolzkk.tistory.com/15 를 참고하자.

*EOF에 대한 개념도 알지 못한 것을 보아 C언어를 배울 때 코드를 따라 쓰는 것만 해서인가 각 코드의 개념에 대해서는 공부가 부족한 것 같다. C언어부터 C++까지 주요 개념에 대한 복습이 필요할 것 같다.*



## 헝가리안 표기법

자주 쓰는 표기법만 알고 있고 그 외에는 헝가리안 표기법으로 작성하지 않는 듯하여 어떻게 표기하는지 다시 확인해 볼 필요가 있다.



## strcmp 함수

strcmp는 'string compare'의 줄임 표현이며 string.h 가 필요하다.

동일하면 0을 반환하고 동일하지 않으면 0이 아닌 값이 반환된다.

https://blog.naver.com/tipsware/221016574788



## strcpy 함수

strcpy는 'string  copy'의 줄임 표현이며 string.h가 필요하다.

복사할 원본 문자열은 반드시 끝에 NULL 문자가 포함되어 있어야 한다.

https://blog.naver.com/tipsware/221301499253



## 입출력 버퍼 참고

https://dojang.io/mod/page/view.php?id=763 



## scanf 정수 한자리씩 입력 받는 법

숫자가 연속 되어 입력이 되었을때 `scanf("%1d",&변수);` 를 통해 하나씩 받을 수 있다.

1은 다른 숫자가 들어갈 수 있다.



## 입력 함수

getline 함수 https://jhnyang.tistory.com/107

fgets / gets 함수 

https://8ublictip.tistory.com/7 

> gets() 함수는 최근 표준에서 제외될 정도로 문제가 많은 함수 이므로 여러 단어를 입력 받을 대는 fgets() 혹은 이를 가공하여 쓰자

 [김성엽 블로그](https://m.blog.naver.com/PostView.nhn?blogId=tipsware&logNo=221326391483&proxyReferer=https%3A%2F%2Fwww.google.com%2F)



