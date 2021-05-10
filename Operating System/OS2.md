# 2. OS Protection & System Call
## 1) OS Protection
+ OS는 잘못된 프로그램이 정상적인 프로그램을 망치지 않도록 여러가지 Protection을 제공한다.
+ 첫번째, Dual-Mode Operation을 통해서 user mode와 kernel mode로 나누어서 실행
+ 두번째, I/O Protection으로 user program은 절대 kernel mode에서 실행해야 하는 프로그램에 접근할 수 없도록 제한
+ 세번째, Memory Protection으로 Base register와 Limit register로 메모리 상에서 접근할 수 있는 범위 지정
+ 네번째, Timer로써 특정 자원을 독차지하고 있는 프로그램이 일정 시간이 지나면 중지되도록 설정
+ 이와 같이 여러 OS Protection을 제공하는데 그 중에서도 Daul-Mode Operation, I/O Protection은 System Call과 연관이 있다.

## 2) Daul-Mode Operation
+ 우선, System Call을 알기 위해서는 Dual-Mode Operation이 무엇인지 알아야 한다.
+ Dual-Mode Operation은 OS가 user mode와 kernel mode로 나누어서 동작하는 것으로 각각 하는 일을 따로 나누게 된다.
+ mode bit을 통해서 mode를 바꾸게 된다.
+ 어떤 명령어 같은 경우에는 반드시 특권 명령을 통해서만 실행할 수 있는데 이것이 바로 kernel mode에서만 실행 가능한 명령이다.
+ 예를 들어 시스템 파일, 디스크 파일에 접근하거나 화면에 결과를 보여주는 등의 작업은 반드시 kernel mode에서 실행해야 한다.
+ 위와 같은 작업들을 현재 user mode에서 실행중인 사용자 프로그램이 실행하고 싶다면 특권 명령을 통해서만 실행이 가능하니 OS에게 특권 명령을 수행할 수 있도록(kernel mode의 code를 수행할 수 있도록) 요청을 보내는데 이것이 바로 System Call이다.

## 3) System Call 기본 정의
+ Interrupt의 종류 중 하나로써 파일 입출력, 프로세스 관리, 화면에 결과를 보여주는 등의 작업은 kernel에서 이루어지는데 사용자 프로그램은 user mode로써 kernel에 직접 접근할 수 없기 때문에 OS에게 요청하여 kernel mode의 기능을 수행할 수 있도록 요청하는 것을 System Call이라고 한다.

## 4) System Call 과정(read() 파일 읽기를 호출했다고 가정)
1) API에는 사용자 프로그램이 호출할 수 있는 수많은 함수들이 정의되어 있는데 우선 API에 있는 read() 호출<br>
2) API의 read()는 라이브러리(lib)의 read()를 호출하면서 System Call 번호(read()에 해당하는), read() 호출시 필요한 parameter들을 register에 저장(각 인터럽트는 고유의 번호를 가지고 있고 그 번호는 Interrupt Vector table에서의 index 번호)<br>----------여기서부터 kernel mode-------------<br>
3) System Call의 Interrupt번호는 128로 고정<br>
4) kernel은 Interrupt Vector table의 128 위치로 가서 System Call() 함수 찾음(System Call() 함수의 시작 주소로)<br>
5) System Call()에 대한 Interrupt Service Routine(Interrupt Handler) 수행<br>
6) kernel은 register에 저장되어 있는 System Call 번호, parameter를 검증하고 stack에 저장(register->memory)<br>
7) 검증결과 정상이면 System Call table(각 System Call에 해당하는 코드들 저장)에서 해당 System Call 번호(지금은 read()에 해당하는)에 맞은 System Call Handler 호출<br>
8) read Handler 함수 수행(Handler는 특정 이벤트를 처리해주는 함수로써 여기서는 read()에 해당하는 작업을 처리)<br>----------kernel mode 끝----------
9) read Handler가 수행되면 다시 user mode로 전환

<br>
[참고자료] Operating System Principles(7th Edition) by Silberschatz et al.
