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
+ 만약, P3, P2, P1 순서대로 왔다면 각각의 waiting time은 P3=0, P2=3, P3=(3+3)=6이고 평균 waiting time은 (0+3+3)/3=2가 된다. 이렇듯, burst time이 긴 process가 먼저 수행되면 다른 process들이 전부 기다리면서 waiting time이 증가하여 평균 waiting time이 증가하게 되는 Convoy Effect가 발생하게 된다.

2. SJF(Shortest Job First)
+ 현재 ready queue에 있는 process 중에서 burst time이 가장 짧은 process 먼저 CPU 할당받는 방식
+ 즉, 먼저 도착했어도 burst time이 더 짧은 process가 있다면 그 process 먼저 CPU 할당받는 방식
+ 비선점형, 선점형 둘다 가능하며 선점형일 경우 SRTF(Shortest Remaining Time First)라고 한다.
![캡처](https://user-images.githubusercontent.com/17876424/117763134-3ecd1200-b265-11eb-855b-34be8c464f2d.PNG)

+ 위의 이미지에서 waiting time은 P1=0, P3=7-4=3, P2=(7+1)-2=6, P4=(7+4+1)-5=7이고 평균 waiting time은 (0+3+6+7)/4=4가 된다.

3. Priority
+ 우선순위가 높은 process가 먼저 CPU 할당을 받는 방식
+ 비선점형, 선점형 둘다 가능하며 FCFS, SJF가 결국 priority를 도착 시간, 남은 시간으로 하는 비선점형 prioirty scheduling이라고도 할 수 있다.
+ Priority 대로 한다면 우선순위가 높은 process가 계속 ready queue에 들어오게 되면 우선순위가 낮은 process는 CPU 할당이 계속 밀리게 되어 CPU 할당을 받지 못하게 되는 starvation이 발생할 수 있다.
+ 이런 starvation을 해결하는 방법이 aging으로써 일정 시간이 지나면 ready queue에 있는 process의 우선 순위를 일정량 높이는 방법을 말한다.
![캡처](https://user-images.githubusercontent.com/17876424/117764184-0a5a5580-b267-11eb-9ee5-35e8c2aa12f3.PNG)

+ 위의 이미지에서 waiting time은 P2=0, P5=1, P1=(1+5)=6, P3=(1+5+10)=16, P4=(1+5+10+2)=18이 되고 평균 waiting time은 (0+1+6+16+18)/5=8.2가 된다.

## 5) Preemptive(선점형) scheduler
1. SRTF(Shortest Remaining Time First)
+ Burst time 중 Remaining time이 짧은 순서대로 process를 수행
+ 만약 현재 CPU 할당중인 process의 remaining time보다 짧은 burst time을 가진 process가 들어온다면 그 process에게 CPU 할당이 이루어지게 된다.
+ 비선점형에서 설명한 SJF의 선점형 방식

2. Round Robin(RR)
+ 각각의 process는 CPU time을 일정하게 나눈 unit time을 할당받아서 수행(Time Quantum)
+ 할당받은 unit time이 다 지나면 process 작업이 완료되지 않아도 preempted되어 다른 process 수행
+ 모든 process가 순서대로 돌아가면서 진행되고 마지막 process가 끝나면 다시 처음 process로 돌아와서 같은 작업을 반복 수행
+ Time Quantum이 길어지게 되면 FCFS와 같고 너무 짧게 되면 context switch가 잦아져서 overhead가 커진다.
![캡처](https://user-images.githubusercontent.com/17876424/117766582-c10c0500-b26a-11eb-9296-d0aaa240af58.PNG)

3. MultiLevel Queue
+ 여러 개의 ready queue를 두고 각각의 우선순위가 있고 ready queue마다 다른 scheduling algorithm을 사용하는 방식
+ process들 역시 알맞는 ready queue에 들어가게 되고 한번 들어간 ready queue에서 다른 ready queue로 이동되지 않는 방식
+ ready queue마다 우선 순위가 다르기 때문에 우선 순위가 낮은 ready queue의 경우에는 starvation이 발생할 수 있다.

4. MultiLevel Feedback Queue
+ MultiLevel Queue에서는 process가 한번 ready queue에 들어가면 이동이 불가능했지만 여기서는 다른 ready queue로 이동이 가능하다.
+ 따라서 MultiLevel Queue에서 발생한 starvation 문제를 이러한 aging 기법을 통해서 해결할 수 있다.

[참고자료] Operating System Principles(7th Edition) by Silberschatz et al.
