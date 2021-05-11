# 8. Process vs Thread
## 1) Program vs Process vs Thread
+ Program: 실행 가능 명령어의 집합, 디스크에 존재
+ Process: 메모리에 적재되어 CPU의 할당을 받아 실행 중인 프로그램
+ Thread: Process 내에서 동작되는 여러 작업의 흐름으로써, Process의 실행 작업 단위

## 2) MultiProcessing vs MultiThreading
+ MultiProcessing: 하나의 응용 프로그램이 여러 개의 Process로 구성되어 각각의 Process가 하나의 작업을 처리하게 되는 것
+ MultiThreading: 하나의 Process가 여러 개의 Thread로 구성되어 각 Thread가 하나의 작업을 처리하는 것
+ 둘다 작업 처리를 위해서는 CPU 할당을 받아야 한다.

## 3) 구조
+ Process: 각각의 Process는 stack, heap, code, data, files, register를 가지고 있다.
+ Thread: 각각의 Thread는 stack, register를 가지고 있고 code, data(heap), files은 공유 메로리에 존재한다.
+ 각각의 Thread가 stack을 가지고 있는 이유는 stack에는 함수 parameter, return값, local variable을 가지고 있기 때문에 각각의 Thread가 각자의 함수 호출이 가능하다는 것
+ 각각의 Thread가 register를 가지고 있는 이유는 각각의 연산 결과나 Program counter 값을 저장을 해야 만약 switch가 일어나게 되었을 때 어디까지 수행되고 중간 결과가 무엇인지 각각의 Thread에 대해서 알아야 하기 때문이다.

## 4) switch
+ Process: Process의 정보는 PCB에 있으며(Thread에 대한 정보도 포함) 다른 Process를 수행하기 위해서는 PCB가 교체되는 Context Switch가 일어나야 하는데 overhead가 크다.
+ Thread: 하나의 Process 내부에서 일어나기 때문에 Context Switch가 발생하지 않으며 각각의 Thread는 stack, register만을 가지고 있기 때문에 이것만 switch가 일어나면 되어서 overhead가 작다. 

[참고자료] Operating System Principles(7th Edition) by Silberschatz et al.
