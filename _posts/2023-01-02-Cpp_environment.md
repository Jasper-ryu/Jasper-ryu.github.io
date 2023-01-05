---
layout: single
title:  "VSCODE에서 C/C++ 개발환경 설정"
categories: research
tag: [vscode, c, c++]
toc: true
author_profile: false
sidebar:
    nav: "docs"
---

## VSCODE(Visual Studio Code)에서 C/C++ 개발해보자

#### Visual Studio Code 공식홈페이지 접속

![](D:\Capture\2023-01-05-11-12-52-image.png)

[(https://code.visualstudio.com/docs/cpp/config-mingw)](vscode 공식홈페이지)

#### MSYS2를 통한 Mingw-w64 설치

![](D:\Capture\2023-01-05-11-16-49-image.png)

[(https://www.msys2.org/)](msys2 공식 홈페이지)

##### 다운 -> 실행 -> 설치 -> 업데이트 -> GCC 설정 -> 환경변수 설정

![Second screen of MSYS2 installation](https://www.msys2.org/images/install-2-path.png)

![Third screen of MSYS2 installation](https://www.msys2.org/images/install-3-finish.png)

![Empty MSYS2 terminal window](https://www.msys2.org/images/install-4-terminal.png)

설치가 완료되면 UCRT64가 실행된다

여기서 아래 코드를 이용하여 core system을 업데이트한다

```cpp
pacman -Syu
```

설치되면 자동으로 꺼진다

![](D:\Capture\2023-01-05-11-31-23-image.png)

시작메뉴에서 "MSYS2 MSYS"를 실행하여 같은 코드를 이용해 같은과정을 반복한다.

```cpp
pacman -Syu
```

이제 업데이트가 끝났으므로 아래 코드를 입력하여 Mingw-w64 toolchain을 설치한다.

```cpp
pacman -S --needed base-devel mingw-w64-x86_64-toolchain
```

마지막으로 환경변수를 설정해주자

```parser
C:\msys64\mingw64\bin
```

재부팅을 추천하지만 재부팅을 하지 않아도 되긴한다 (안되면 재부팅)

![](D:\Capture\2022-11-29-07-48-12-image.png)

터미널에서 설정이 잘되어있는지 확인!

```parser
gcc --version
```

```parser
g++ --version
```

```parser
gdb --version
```

![](D:\Capture\2023-01-05-11-29-35-image.png)

C++ 파일 아무거나(test.cpp) 만들면 C/C++ extenstion을 설치하라는 창이 뜬다

![](D:\Capture\2023-01-05-11-36-03-image.png)

3개 다 설치를 해주고 설정을 하자

![](D:\Capture\2023-01-05-11-34-04-image.png)

컴파일러 경로를 설치한 msys의 mingw64 g++로 하고 intellisense 모드를 windows-gcc-x64로 설정

마지막으로 c와 c++ 표준을 설정하면 된다

![](D:\Capture\2023-01-05-11-37-53-image.png)

----------------------------------------------

여기까지가 공식홈페이지 설치과정 그대로

----------------------------------------------

빌드 컴파일 디버그가 잘된다고 해서 바로 F5를 눌러보지만!!!!

역시나 오류가 발생!!

오류를 잡기위해 "C:\msys64\mingw64\bin" 가서 "libstdc++-6.dll" 파일을 복사해서 "C:\Windows\System32"에 복사하면

잘된다.. 아주 잘된다..

Extensions > code runner (검색) > install

File > Preferences > Settings > run in terminal (검색)

Code-runner: Run in Terminal (옵션 체크)

이렇게 하면 C/C++에 대한 설정이 모두 끝난다.
