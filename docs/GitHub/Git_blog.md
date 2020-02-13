<img src="https://img.shields.io/badge/Update-20.01.14-blue" align = "left">

#### Gitblog post 오류 수정

오류 : 블로그에 글은 올라갔는데 타이틀과 태그, 카테고리 적용이 안됨

해결 : 전에 작성한 글과 비교했을때  머리말(YAML 머리말 블록)을 잘못 작성하였다는 것을 확인하였다.

```
---
layout: post
title: Blogging Like a Hacker
---
```

- 파일의 맨 첫부분에 위치
- 시작과 끝을 대시문자 세 개로 감싸서 올바른 YAML 형식으로 작성해야한다.

- [Jekyll frontmatter 설명](https://jekyllrb-ko.github.io/docs/frontmatter/)



<img src="https://img.shields.io/badge/Update-20.01.18-blue" align = "left">



- 링크가 안 걸리는 것
  - [] () 를 이용해서 다시 눌렀을 때 링크로 이동되도록 수정했다.
- 타이틀 적용이 안 되는 것
  - YAML 머리말 블록 잘 못 작성, 올리기 전에 다시 한번 확인할 것
- 포스트의 코드 펜스 적용이 안 되는 것
  - 코드 펜스 언어에 C++이라고 적은 것만 적용이 안 되었고 c++이라고 적은 것은 적용되는 것으로 확인되었다.

