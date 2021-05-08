# 1. Introduction
## 1) 운영체제란?
+ 운영체제란 사용자와 하드웨어 사이의 소통을 도와주는 소프트웨어를 말한다.
+ 운영체제는 모든 하드웨어(기계장치)와 소프트웨어(프로그램)을 관리한다.
+ 운영체제의 중심에는 가장 핵심 역할을 하는 Kernel이 있고 그 주위에 user interface가 있는 구조로 되어있다.
## 2) 기본적인 컴퓨터 구조
+ 시스템 버스를 중심으로 CPU, 메모리, 여러 device들이 연결되어 있다.
+ 각각의 device들은 device controller에 의해서 관리되며 각각의 device controller에는 device에 필요한 데이터가 저장되어 있는 local buffer가 있다.
+ 기본적으로 데이터의 흐름은 버스를 통해서 Memory-CPU-Device controller 의 관계로 이루어져 CPU에 의해 관리된다.
## 3) Interrupt의 정의
+ Interrupt란 CPU의 현재 업무를 중단하고 CPU의 즉각적인 처리를 필요로 하는 이벤트를 처리하기 위해 HW/SW로부터의 요청을 말하며 Trap 이라고도 불린다.
+ 또한, Interrupt는 예외상황이 발생했을 때 즉각적인 처리를 하기 위해 사용하는 것을 말한다.
+ HW Interrupt와 SW Interrupt로 나눌 수 있다.
## 4) HW Interrupt
+ 여러 하드웨어 장치들이 CPU의 서비스를 받아야 할 때 발생
+ 각각의 하드웨어 장치들은 IRQ(Interrupt Request) line을 가지고 있고 이를 통해 CPU에게 전달
+ 대표적으로 I/O device의 입출력 요청이 있다.
## 5) SW Interrupt
+ 프로그램의 잘못된 연산이나 사용자의 요청에 의해 CPU의 서비스를 받아야 할 때 발생
+ Interrupt가 발생하면 먼저 Memory에 있는 Interrupt Vector table를 찾는다
+ Interrupt vector라는 것은 여러 종류의 Interrupt에 대한 시작 주소를 말하고 이것들을 모아놓은 것을 Interrupt Vector table이라고 한다.
+ Interrupt Vector table에서 현재 발생한 Interrupt의 시작 주소를 찾으면 메모리상의 그 시작 주소로 가는데 그 시작 주소에는 Interrupt 실행 코드인 Interrupt Service Routine 존재
+ Interrupt Service Routine은 Interrupt Handler라고도 하며 Interrupt 발생 시 수행해야 하는 코드를 말한다.
+ Interrupt Service Routine(Interrupt Handler) 수행을 마치면 CPU는 다시 자신이 하던 업무로 돌아가며 Interrupt를 마친다.
+ 대표적으로 Segmentation fault, System call이 있다.
## 6) Interrupt에서 OS의 역할
+ Interrupt가 발생하면 현재 CPU의 상태를 저장해야 하는데 이를 저장하기 위한 자료구조를 OS의 kernel이 제공한다.
## 7) DMA(Direct Memory Access) 란
+ 기본적인 컴퓨터 구조에서 device controller가 메모리 접근을 하기 위해서는 반드시 CPU의 명령을 통해서 이루어져야 하는데 그러기 위해서는 Interrupt를 해야 한다.
+ Interrupt를 한다는 것은 CPU의 현재 업무를 중지해야 하는 상황이며 그럴 경우 CPU 사용의 효율성이 떨어지며 고속 처리도 불가능해진다.
+ 따라서 DMA는 device controller가 CPU Interrupt 없이 메모리에 직접 접근할 수 있도록 하는 것을 말한다.

<br>

[참고자료] Operating System Principles(7th Edition) by Silberschatz et al.
