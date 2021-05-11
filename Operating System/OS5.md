# 5. Fork()
## 1) Fork()
+ fork()는 새로운 process를 create하는 시스템 콜이다.
+ 새로운 process를 생성하는 process를 부모 process, 부모 process에 의해서 새롭게 생성되는 process를 자식 process라고 한다.
+ fork()를 통해 새로운 process를 생성하면 fork() 이후의 명령어 집합이 똑같이 copy되어 새로운 process가 생성된다.

## 2) 부모, 자식 process 구분
+ 부모 process, 자식 process는 똑같은 명령어 집합을 가지고 있기 때문에 부모이냐 자식이냐에 따라서 실행되는 코드가 달라야 한다.
+ 부모 process의 경우, fork()의 return 값이 자식 process id
+ 자식 process의 경우, fork()의 return 값이 0 

## 3) exec()
+ 자식 process의 명령어 집합은 exec()를 통해서 새로운 program으로 덮어쓸 수 있으며 이것은 메모리 내용을 새로운 program으로 교체하는 것을 의미

## 4) exit(status)
+ process가 마지막 명령어를 수행하면 exit(status)를 통해서 종료

## 5) wait(&status)
+ 부모 process는 자식 process가 수행을 종료할 때까지 기다렸다가 자식 process의 수행이 종료되면 status value를 wait()로부터 받는다.

## 6) Zombie Process
+ 자식 process가 수행을 종료하면 부모 process는 wait(&status)를 통해서 status value가 회수되고 완전히 사라져야 하는데 아직 부모 process의 작업이 종료되지 않아 wait()를 호출하지 않아서 남아있는 상태.
+ 간단히 말해서 부모는 살아있는데 자식이 죽은 경우
+ 모든 process들은 아주 잠깐동안 zombie process가 될 수 있으며 부모 process 작업이 완료되어 wait()를 호출하면 자식 process는 정상적으로 종료된다.

## 7) Orphan Process
+ 자식 process는 아직 수행이 완료되지 않았는데 부모 process가 wait()를 호출하지 않고 그냥 terminated 되었을 때의 자식 process의 상태를 말한다.
+ 간단히 말해서 자식은 살아있는데 부모가 죽은 경우
+ 이 경우, init process가 주기적으로 wait를 호출하여 Orphan process 상태에 있는 자식 process들의 status를 회수하게 된다.

[참고자료] Operating System Principles(7th Edition) by Silberschatz et al.
