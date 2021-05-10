# 4. Context Switch
## 1) Multiprogramming & Multitasking
+ Context Switch에 대해 알기 전에 간단하게 Multiprogramming과 Multitasking을 정리하고자 한다.
+ Multiprogramming: 하나의 program으로는 CPU나 I/O 장치를 항상 바쁘게 만들 수 없기 때문에 미리 메모리에 많은 program을 올려두고 지속적인 transition이 일어나도록 하는 것
+ Multitasking: Process는 CPU 자원 할당을 받아 실행되는데 메모리 속 여러 program들이 빠르게 switch되면서 CPU 자원 할당을 받으면서 마치 여러 program이 동시에 수행되는 것처럼 보이게 하는 것.
+ 여기서 CPU 자원 할당을 받는 process가 switch되는데 process가 switching 되는 작업이 Context Switch

## 2) Context Switch란
+ CPU의 자원을 할당받아 process가 switch되기 위해서는 현재 실행중이던 process의 상태를 저장하고 새로운 process의 상태를 가져와야 하는데 이것을 Context Switch라고 한다.
+ 여기서 Context가 process의 상태이자 정보인데 이것은 PCB(Process Controll Block)에 저장되어 있다.
+ 즉, Context Switch가 일어난다는 것은 Process의 PCB를 switch하는 것.
+ 정리하면, CPU가 현재 실행중인 process의 상태를 PCB에 저장하고 새롭게 실행할 process의 상태를 PCB로부터 가져와서 register에 적재하는 과정.

## 3) Context Switch overhead
+ 보통 Interrupt가 발생할 때 Context Switch가 발생하는데 이때 Overhead가 발생한다.
