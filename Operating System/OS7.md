# 7. Thread
## 1) Thread의 정의
+ 기본적으로 Thread라는 것은 Process 내에서 실제로 실행되는 작업의 흐름 단위를 말한다.
+ 하나의 Process에는 많은 Thread가 존재하고 최소 1개의 Thread를 가지고 있다.
+ 각각의 Thread는 각자의 register와 stack을 가지고 있다.
+ code, data, files, heap은 공유한다.
+ Process만으로 구성되어 있을 때는 context switch로 인하여 overhead가 발생하지만 하나의 Process가 여러 Thread로 구성되어 process의 switch가 아니라 process 내부에서 Thread간의 switch가 일어나기 때문에 overhead가 적다.
+ 각각의 Thread: register, stack
+ 공유 메모리: code, data, files, heap

## 2) MultiThreading
+ MultiThreading이라는 것은 하나의 process가 여러 개의 thread로 구성되어 각 thread가 하나의 작업을 처리하는 것이다.
+ MultiThreading은 single processor(CPU)인 경우와 multiple processors(CPU) or cores인 경우로 나누어 생각할 수 있다.

## 3) MultiThreading(single processor)
+ 결국 Thread가 작업을 수행하기 위해서는 CPU 자원 할당을 받아야 하는 것은 process와 같다.
+ CPU가 하나이기 때문에 한번에 하나의 Thread만이 작업을 수행한다.
+ 하지만 MultiThreading이기 때문에 thread간의 switch가 되어 마치 여러 작업이 동시에 이루어지는 것처럼 보이게 한다.(illusion of parallelism, achieve of concurrency)

## 4) MultiThreading(multiple processor or cores)
+ processor 혹은 cores(각종 연산을 하는 CPU의 핵심 역할, 요즘은 multicore가 대세)인 경우 각각의 Thread가 각각 processor(CPU) 혹은 core를 할당받는다
+ 실제로 공유 메모리를 통해서(code, data, files) 각각의 작업이 동시에 이루어진다.(parallelism) 

## 5) Thread pool & Thread Local Storage
+ Thread가 필요할 때마다 create하면 overhead가 발생하니 미리 여러 개의 Thread를 만들어놓고 필요할 때 깨워서 사용하기 위해 만들어둔 것이 Thread pool
+ 공유 메모리에서 data를 공유하지만 Thread마다 각자 data를 필요로 하는 경우가 있는데 이를 위해서 TLS(Thread Local Storage)를 선언하고 공유 메모리의 data를 copy하여 각자 사용할 수 있다.
