# Thread 개념
> 실행 중인 하나의 애플리케이션을 프로세스(process)라고 부르며, 프로세스 내에서 두 가지 이상의 작업을 처리
> 하는 것을 멀티스레드(multi thread) 라고 부른다.

#### 프로세스와 스레드
프로세스들은 운영체제에서 할당받은 자신의 메모리를 가지고 실행하기 때문에 서로 독립적이다. 따라서
하나의 프로세스에서 오류가 발생해도 다른 프로세스에게 영향을 미치지 않는다. 하지만 <b>멀티 스레드는 하나의
프로세스 내부에 생성되기 때문에 하나의 스레드가 예외를 발생시키면 프로세스 자체가 종료</b>될 수 있어 다른 스레드에게
영향을 미치게 된다.

#### 스레드 생성 방식
1. java.lang.Thread 클래스 객체화 방식  
    - Runnable을 매개값으로 갖는 생성자를 호출해야함
    - Runnable이란 스레드가 실행할 수 있는 코드를 가지고 있는 객체라고 해서 붙여진 이름
    - `start()` 메소드가 호출되면, 작업 스레드는 매개값으로 받은 Runnable의 run() 메소드를 실행  
    - 
        ```
        public class Task implements Runnable{
            @Override
            public void run() {
                System.out.println("thread test");
            }
        }
      
        ...
      
        Runnable task = new Task();
        Thread thread = new Thread(task);
        thread.start();      
        ```
        ```
        // 코드를 줄이기 위해 익명 객체를 매개값으로 사용할 수도 있다.
        Thread thread = new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("thread test");
            }
        });
      
        thread.start();
        ```
2. Thread 상속 방식
     - 스레드가 실행할 작업을 Runnable로 만들지 않고 Thread의 하위 클래스로 스레드를 정의하면서 작업 내용을 포함 시키는 방법
     - Thread 클래스 상속한 후 run 메소드를 재정의해서 스레드가 실행할 코드를 작성
     - 
        ```
        public class Task extends Thread{
            @Override
            public void run() {
                System.out.println("스레드 테스트");
            }
        }
       
       ...
       
       Thread thread = new Task();
       thread.start();
       
        ``` 
       ```
       // 코드를 줄이기 위해 익명 객체로 스레드 객체 생성할 수도 있다.
       Thread thread = new Thread(){
           @Override
           public void run() {
               System.out.println("스레드 테스트");
           }
       };

       thread.start();
       ```
#### 스레드 이름

 - 스레드는 고유의 이름을 가지고 있으며, 디버깅 시 어떤 스레드가 어떤 작업을 하는지 조사할 목적으로
 사용되곤 한다.
 - 메인 스레드는 `main`이라는 이름을 가지고 있으며, 생성되는 스레드는 자동적으로 `Thread-n`이라는 이름으로
 설정된다.(n은 스레드 번호를 의미)
    - 직접 이름을 설정하고 싶다면 `setName()` (인스턴스 메소드이므로 객체 참조 필수)
    - 이름을 확인하고 싶다면 `getName()` (인스턴스 메소드이므로 객체 참조 필수)
    
#### 스레드 우선순위

 - 멀티 스레드는 동시성(Concurrency)와 병렬성(Parallelism)으로 실행됨
    - 동시성 : 멀티 작업을 위해 하나의 코어에서 멀티 스레드가 번갈아가며 실행하는 성질
    - 병렬성 : 멀티 작업을 위해 멀티 코어에서 개별 스레드를 동시에 실행하는 성질 
 - 스레드의 개수가 코어의 수보다 많을 경우, 스레드를 어떤 순서에 의해 동시성으로 실행할 것인가를
 결정해야 하는데, 이것을 `스레드 스케줄링`이라고 한다. 스레드 스케줄링에 의해 스레드들은 아주 짧은 시간에 번갈아가면서
 `run()` 메소드를 조금씩 실행하는 것
 - 우선순위(Priority) 방식 : 우선순위가 높은스레드가 실행 상태를 더 많이 가지도록 스케줄링
    - 개발자 코드 제어 가능
    - `Thread.setPriority(우선순위)`
    - `Thread.setPriority(Thread.MAX_PRIORITY)` // 10
    - `Thread.setPriority(Thread.NORM_PRIORITY)` // 5
    - `Thread.setPriority(Thread.MIN_PRIORITY)` // 1
 - 순활할당(Round-Robin) 방식 : 정해진 시간만큼 실행하는 방식
    - JVM에 의해서 정해지기 때문에 코드제어 불가
    
#### 동기화 메소드와 동기화 블록
멀티 스레드 환경에서는 스레드들이 객체를 공유해서 작업하는 경우가 많다. 이 경우 의도하지 않은 상태
변경이 일어날 수 있기 때문에 하나의 동기화 작업을 해주어야 한다.

 - synchronized 키워드 메소드에 적용
    - ```
      public synchronized void setSleep(int i) {
        ...
      }  
      ```
 - synchronized
     - ```
       public void setSleep(int i) {
         synchronized (this) {
           ...
         }
       }  
       ```