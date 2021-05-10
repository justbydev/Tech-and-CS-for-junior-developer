# 3. Process
## 1) Process의 정의
+ Program은 디스크에 저장되어 있는데 이런 Program이 메모리에 적재되어 실행중인 상태가 될 때 Process라고 한다.

## 2) Process State
1) new: process 생성
2) ready: 메모리에 적재된 후 CPU에게 할당되어야 실행할 수 있는데 CPU에게 실행되기를 대기하는 상태
3) running: process 실행
4) terminated: process 종료
5) waiting: I/O 요청이 필요하거나 다른 event가 발생했을 때, 그것을 기다리고 있는 상태

## 3) Process 흐름
1) process가 생성된 후 종료할 때까지(waiting 없다면)
- new->ready->scheduler에 의해 CPU 할당->running->process 작업 완료->terminated
2) process가 생성된 후 I/O 요청 필요
- new->ready->scheduler에 의해 CPU 할당->running->I/O service 필요->waiting->ready->1.의 과정이나 2.의 과정 반복

## 4) PCB(Process Control Block)
+ 각 process에 대한 정보가 저장되어 있는 block이 PCB
+ 각 process는 OS에서 PCB로 표현
+ process state, number, program counter, CPU register, thread information 등 process의 정보가 모두 표현

<br>
[참고자료] Operating System Principles(7th Edition) by Silberschatz et al.
