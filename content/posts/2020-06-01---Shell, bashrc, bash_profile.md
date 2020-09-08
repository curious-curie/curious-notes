---
title: Shell, bashrc, bash_profile?
date: "2020-06-01T22:40:32.169Z"
template: "post"
draft: false
slug: "shell-bashrc"
category: "CS"
tags:
  - "CS"
  - "general"
description: "환경변수 지정할 때 .bashrc, bash_profile 등 얘기가 나오는데 생각없이 쓰다가 도대체 이것들이 뭔가... 싶어서 정리해본 글.
"
---

# Shell, bashrc, bash_profile

환경변수 지정할 때 .bashrc, bash_profile 등 얘기가 나오는데 생각없이 쓰다가 도대체 이것들이 뭔가... 싶어서 정리해본 글.

## Kernel

운영 체제의 핵심 부분

소프트웨어와 하드웨어 간의 커뮤니케이션 관리 

> 운영체제에서 가장 중요한 구성요소로서 입출력을 관리하고 소프트웨어로부터의 요청을 컴퓨터에 있는 하드웨어(CPU, 메모리, 저장장치등)가 처리 할 수 있도록 요청을 변환하는 역할을 한다

[커널(Kernel)과 쉘(Shell)](https://jinshine.github.io/2018/05/10/%EC%BB%B4%ED%93%A8%ED%84%B0%20%EA%B8%B0%EC%B4%88/%EC%BB%A4%EB%84%90(Kernel)%EA%B3%BC%20%EC%89%98(Shell)/)

## Shell

운영체제와 커널을 이어주는 역할

운영체제 바깥쪽에서 명령어를 해석해서 커널에 전달해주는 역할 

### bash

Bourne Again Shell (기존 unix shell program인 sh의 enhanced version)

리눅스에서 가장 널리 사용되는 쉘

- /etc/profile
- /etc/bashrc
- ~/.bash_profile
- ~/.bashrc
- ~/.bash_logout

출처: [https://originalchoi.tistory.com/19](https://originalchoi.tistory.com/19)


- Interactive Shell

non-option arguments 없이 실행된 shell 

사용자로부터 프롬프트를 통해 직접 명령을 입력받아 실행

- Non-interactive Shell

작성한 script 파일을 실행시키는 것 등

- Login shell
- Non-login shell

- **Invoked as an interactive login shell, or with --login**

* 여기서 login shell? 사용자가 로그인했을 때 적용되는 shell 

interactive login shell로서 (혹은 —login 옵션으로 non-interactive shell로서) Bash 실행 시 /etc/profile 파일 먼저 읽고 실행

/etc/profile 읽은 후 **/.bash_profile,** ~/.bash_login, ~/.profile 탐색하고 그 순서로 읽고 실행

⇒ 콘솔 통해 로그인하면 (ssh 통해서든 컴에 입력해서든) .bash_profile이 실행됨

- **Invoked as an interactive non-login shell**

**~/.bashrc** 읽고 실행 

⇒ 이미 로그인 되어있는 상태에서 새로운 터미널 윈도우 열면 .bashrc가 실행됨.

OSX에선 새로운 탭이나 윈도우를 킬 때마다 login shell 인 것처럼 실행시킨다고 함 ⇒ bash_profile 사용이 권장됨

그리고 이렇게 추가해서 bash_profile에서 bashrc까지 가져오게 하는 게 추천됨

[bash_profile_vs.html](http://www.joshstaiger.org/archives/2005/07/bash_profile_vs.html)

> Most of the time you don’t want to maintain two separate config files for login and non-login shells — when you set a PATH, you want it to apply to both. You can fix this by sourcing .bashrc from your .bash_profile file, then putting PATH and common settings in .bashrc.

```
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
```

references

[https://webdir.tistory.com/126](https://webdir.tistory.com/126)