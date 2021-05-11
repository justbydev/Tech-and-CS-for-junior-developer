# 9. CPU Sheduling
## 1) Scheduling이 필요한 이유
+ Multiprogramming을 통해서 메모리에 많은 process가 있고 Multitasking을 통해서 빠르게 context switch가 일어나면서 CPU 할당을 받는다고 했다.
+ 이렇게 CPU 할당을 받을 때 어떤 process가 받느냐를 결정해야 하는데 이 때문에 Scheduing 기법이 필요하다.

## 2) CPU Scheduler(Preemptive vs Non-Preemptive)
+ CPU 할당을 받아서 실행할 proces를 결정하는 역할을 하는 것이 CPU sheduler
+ preemptive와 non-preemptive로 나누어지게 된다.
+ preemptive는 OS가 CPU를 먼저 선점하여 현재 CPU 할당을 받은 process의 작업이 끝나지 않거나 I/O, 인터럽트가 발생하지 않았어도 OS에 의해서 강제로 다른 process로 switch되는 것을 말한다.
+ non-preemptive는 현재 CPU 할당을 받은 process의 작업이 끝나거나 I/O나 인터럽트가 발생하기 전까지 다른 process에 의해서 CPU 선점을 뺏기지 않는 것을 말한다.

## 3) Scheduling Criteria
1. CPU utilization: 지속적으로 process를 할당하여 CPU를 바쁘게 만드는 것
2. Throughput: 단위 시간당 몇 개의 process 작업을 끝낼 수 있는가
3. Turnaround time: 특정 process가 요청된 후 ready queue에 들어가면서부터 process를 완료할 때까지의 시간
4. Waiting time: 특정 process가 ready queue에 대기하는 시간
5. Response time: 특정 process가 요청된 이후 응답이 시작될 때까지 걸리는 시간
+ CPU scheduler는 CPU utilization, throughput는 maximize하고 turnaround time, waiting time, response time은 minimize하는 것을 목표로 한다.

## 4) Non-preemptive(비선점형) scheduler
1. FCFS(First Come First Served)
+ ready queue에 먼저 들어온 process를 먼저 CPU 할당받는 방식
+ 비선점형이기 때문에 CPU 할당받은 process 작업이 완료되면 다른 process가 다시 할당받는다.
![캡처](https://user-images.githubusercontent.com/17876424/117744772-357f7d80-b244-11eb-8943-342be5a05a76.PNG)

+ 위의 이미지는 process가 P1, P2, P3 순서대로 ready queue에 도착한 것을 나타내는 Gantt Char.<br>
+ 각각의 waiting time은 P1=0, P2==24, P3=(24+3)=27이고 평균 waiting time은 (0+24+27)/3=17이 된다.
