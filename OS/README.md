***([참고1](https://github.com/WooVictory/Ready-For-Tech-Interview), [참고2](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/OS), [참고3](https://github.com/pparkcoder/TechnicalNote)을 바탕으로 작성하였으며, 꾸준하게 추가할 예정)***

<br>

##### 정리 순서

1. [메모리 구조](https://github.com/pparkcoder/CS-study/tree/master/OS#%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%ACscheduler) - **완료**
2. [프로세스, 스레드](https://github.com/pparkcoder/CS-study/tree/master/OS#%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%ACscheduler) - **완료**
3. [Context Switching](https://github.com/pparkcoder/CS-study/tree/master/OS#%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%ACscheduler) - **완료**
4. [CPU 스케줄링 관련](https://github.com/pparkcoder/CS-study/tree/master/OS#%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%ACscheduler) - **완료**
5. [동기화, 비동기화 관련](https://github.com/pparkcoder/CS-study/tree/master/OS#%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%ACscheduler) - **진행 중**
6. 메모리 관리 (페이징 등)
7. 메모리 단편화
8. 캐시

<br><br>

# 메모리 구조

![](https://user-images.githubusercontent.com/21440957/64079882-6cd82000-cd28-11e9-8810-2bfe3a4944ef.png)

<br>

#### 코드 영역

- 실행할 프로그램의 코드가 저장되는 영역 = 텍스트 영역
- CPU는 코드 영역에 저장된 명령어를 하나씩 가져와서 처리

<br>

#### 데이터 영역

- 프로그램의 전역변수와 정적변수가 저장되는 영역
- 데이터 영윽은 프로그램의 시작과 동시에 할당, 프로그램 종료 시 소멸

<br>

#### 힙 영역

- 사용자에 의해 메모리 공간이 동적으로 할당되고 해제
- C/C++ -> malloc, free, 등
- Java -> **가비지 컬렉터**가 자동으로 해제해 줌
- 메모리의 낮은 주소 에서 높은 주소 방향으로 할당
- 런타임 시 크기가 결정 됨

<br>

#### 스택 영역

- 함수의 호출과 관계되는 지역변수 와 매개변수가 저장되는 영역
- 함수의 호출 완료 시 소멸
- 메모리의 높은 주소 에서 낮은 주소 방향으로 할당
- 컴파일 시 크기가 결정 됨

<br>

#### 힙 과 스택

- 두 영역은 같은 공간을 공유
- 힙은 메모리의 낮은 주소 (위쪽) 부터 할당, 스택은 메모리의 높은 주소 (아래쪽)부터 할당
- 힙 영역이 크면 스택 영역이 작아지고, 스택 영역이 크면 힙 영역이 작아짐

<br><br>

# 프로세스 vs 스레드

### 프로그램

- 어떤 작업을 위해 실행할 수 있는 파일을 의미

<br>

### 프로세스(Process)

- **실행 중인 프로그램** 으로 디스크로부터 메모리에 적재되어 **CPU**의 할당을 받은 작업 단위
- **독립된 메모리 영역을 할당 받음**
- 운영체제로부터 시스템 자원을 할당받음
- 할당받는 시스템 자원 
  - CPU 시간
  - 운영을 위한 주소 공간
  - Code, Data, Stack, Heap의 구조로 되어있는 독립된 메모리 영역
- 기본적으로 프로세스마다 최초 **1개**의 스레드를 갖음 => **메인 스레드**
- **한 프로세스는 다른 프로세스의 변수나 자료구조에 접근할 수 없음**
- 접근을 위해서는 프로세스 간 통신 IPC(Inter-Process Communication) 필요
- IPC란 프로세스들 사이에 서로 데이터를 주고받는 행위 또는 방법이나 경로

<br>

### 프로세스 제어 블록(Process Control Block, PCB)

- 특정 프로세스에 대한 중요한 정보를 저장하고 있는 **커널 내의 자료구조**
- 운영체제는 **프로세스의 생성과 동시에 고유한 PCB 생성**
- 프로세스는 CPU를 할당받아 작업을 처리하던 중, 프로세스 전환이 발생하면 **진행하던 작업을 PCB에 저장 후 CPU 반환**
- 다시 CPU를 할당받게 되면 PCB에서 저장된 내용을 불러와 **종료 시점부터 다시 작업 수행**

![](https://t1.daumcdn.net/cfile/tistory/2164D3365829BAD527)

- PCB에 저장되는 정보
  - 프로세스 식별자(Process ID, PID) : 프로세스 식별 번호
  - 프로그램 카운터(Program Counter) : 프로세스가 다음에 실행할 명령어의 주소를 가르킴
  - CPU 레지스터
  - CPU 스케쥴링 정보 : 프로세스의 우선순위, 스케쥴 큐에 대한 포인터 등
  - 메모리 관리 정보(Memory Information) : 페이지 테이블 또는 세그먼트 테이블 등과 같은 정보를 포함
  - 어카운팅 정보(Accounting Information) : 사용된 CPU시간 등
  - 입출력 정보(I/O Information) : 프로세스에 할당된 입출력 장치들과 열린 파일 목록

<br>

### 스레드(Thread)

- **프로세스 내에서 실제로 작업을 수행하는 주체**

- 프로세스의 실행 단위라고 할 수 있으며, 한 프로세스 내에서 동작되는 여러 실행 흐름으로 프로세스 내의 주소 공간이나 자원 공유 가능

![](https://user-images.githubusercontent.com/33534771/77537866-232c6e00-6ee2-11ea-91dc-12dacf688276.png)

- 스레드는 프로세스 내의 Code, Data, Heap 영역은 **다른 스레드와 공유**
  - Code 영역을 공유하기 때문에 한 프로세스 내부의 스레드들은 프로세스가 가지고 있는 함수를 모두 호출 가능
  - Heap, Data 영역을 공유하기 때문에 IPC 없이도 **스레드 간 통신 가능**
- **Stack 영역을 따로 할당 받음** 
  - Stack은 함수 호출 시 전달되는 인자, 되돌아 갈 주소값 및 함수 내에서 선언하는 변수 등을 위한 메모리 공간
  - Stack 영역이 독립적이라는 것은 독립적인 함수 호출이 가능하다는 것이고 이는 독립적인 실행 흐름이 추가되는 것
  - 따라서 독립적인 실행 흐름을 추가하기 위한 최소 조건
- **PC Register를 따로 할당 받음**
  - PC 값은 스레드가 현재 명령어의 어디까지 수행하였는지를 나타냄
  - CPU 반환 시, 명령어가 어느 부분까지 수행되었는지 기억하기 위함

<br>

***프로세스 : 자신만의 고유 공간과 자원을 할당받아 사용하는 작업의 단위***

***스레드 : 프로세스가 할당받은 자원을 이용하는 실행의 단위로, 다른 스레드와 프로세스의 자원과 공간을 공유***

<br>

### 멀티 프로세스(Multi Process)

- 하나의 응용프로그램을 ***여러 개의 프로세스로 구성***하여 각 프로세스가 하나의 작업을 처리하도록 하는 것
- 장점
  - **여러 개의 자식 프로세스 중 하나에 문제 발생 시, 문제가 발생한 자식 프로세스만 죽음 (안전성)**
- 단점
  - Context Switching (문맥 교환) 에서의 오버헤드
    - 프로세스는 각 독립된 메모리 영역을 할당받았기에 공유하는 메모리가 없음
    - 따라서 캐시 메모리 초기화 등 무거운 작업 진행 시, 많은 시간이 소모 되는 등 오버헤드 발생 가능
  - 프로세스 간 통신 IPC(Inter-Process Communication)
    - **한 프로세스는 다른 프로세스의 변수나 자료구조에 접근할 수 없음**
    - 접근을 위해서는 프로세스 간 통신 필요

<br>

### 멀티 스레드(Multi Thread)

- 하나의 응용 프로그램을 ***여러 개의 스레드로 구성***하고 각 스레드가 하나의 작업을 처리하도록 하는 것
- 웹 서버는 대표적인 멀티 스레드 응용 프로그램
- 장점
  - 메모리 공간과 시스템 자원 소모가 줄어듬
  - 스레드 간 통신시, 전역 변수의 공간 또는 동적으로 할당된 공간인 Heap 영역을 이용해 데이터를 주고 받으므로 통신 방법이 간단
  - Context Switching 시, 캐시 메모리를 비울 필요가 없기에 비용이 적고 빠름
  - **따라서** 시스템의 처리량이 향상되고 자원 소모가 줄어들며, 프로그램의 응답 시간 단축
- 단점
  - 서로 다른 스레드가 Data, Heap 영역 등을 공유하기 때문에, 한 스레드가 다른 스레드에서 사용중인 변수나 자료구조에 접근하여 엉뚱한 값을 읽어오거나 수정이 가능. **즉 자원 공유의 문제 발생**
  - 그렇기 때문에, 멀티 스레딩 환경에서는 **동기화 작업이 필요**
  - **하나의 스레드에 문제가 생기면 전체 프로세스에 영향**

<br>

***멀티 스레드 VS 멀티 프로세스***

***멀티 스레드***

- 멀티 프로세스보다 적은 메모리 공간을 차지
- Context Switching이 빠름
- 오류로 인해 하나의 스레드가 종료되면 전체 스레드 종료
- 동기화 문제

<br>

***멀티 프로세스***

- 멀티 스레드보다 많은 메모리 공간과 CPU 시간을 차지
- 오류로 인해 하나의 프로세스가 죽더라도 다른 프로세스에 영향을 끼치지 않음

<br>

=> **이 두가지는 동시에 여러 작업을 수행한다는 점에서 같지만, 적용해야 하는 시스템에 따라 적합/부적합이 구분됨. 따라서 대상 시스템의 특징에 따라 적합한 동작 방식을 선택하고 적용이 필요**

<br>

***멀티 프로세스 대신 멀티 스레드를 사용하는 이유***

![](https://user-images.githubusercontent.com/33534771/77537949-41926980-6ee2-11ea-90eb-569dc64faed5.png)

- 프로그램을 여러 개 키는 것보다 하나의 프로그램 안에서 여러 작업을 해결하는 것이 효율적
- 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 자원을 효율적으로 관리 가능
- Context Switching시, 캐시 메모리를 피울 필요가 없기에 비용이 적고 더 빠름 -> 스레드는 Stack영역만 초기화 하면 되기 때문
- 스레드는 프로세스 내의 메모리를 공유하기 때문에 데이터 전달이 간단하여 IPC에 비해 비용이 적고 더 빠름 -> 스레드는 프로세스의 Stack 영역을 제외한 모든 메모리를 공유하기 때문

<br><br>

# Context Switching

- CPU는 한번에 하나의 프로세스만 처리 가능
- 여러 프로세스를 처리해야 하는 상황에서 현재 진행중인 Task(프로세스, 스레드)의 상태를 PCB에 저장하고, 다음에 진행할 Task의 상태값을 읽어 적용하는 과정
- **즉, 다른 프로세스에게 CPU를 할당해 작업을 수행하는 과정**
- 한 프로세스의 상태는 그 프로세스의 프로세스 제어 블록(PCB)에 기록
- Context Switching 동안에는 다른 작업을 수행할 수 없기 때문에, Context Switching 시간은 오버헤드라고 할 수 있음
- 많은 비용 소모
  - Cache 초기화
  - Memory mapping 초기화
  - 커널 항상 실행
- Context Switching 비용 : 프로세스 > 스레드 
  - 스레드는 Stack 영역을 제외한 모든 메모리를 공유하기 때문에 Stack 영역만 변경하면 됨



![](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/684074/0f1e8498-9405-95aa-e2b9-7ef1f3d0e6e9.png)

<br>

### 진행 과정

1. Task의 대부분 정보는 Register에 저장되고 PCB로 관리
2. 현재 실행하고 있는 Task의 상태를 PCB에 저장
3. 다음 실행할 Task의 PCB 정보(프로그램 카운터 등) 을 읽어 Register에 적재 후, CPU가 이전에 진행했던 과정을 연속적으로 수행

<br>

### 발생 시점

1. 멀티태스킹
   - Task가 하나의 프로세서 상에서 운영체제의 스케줄링 방식에 따라 조금씩 번갈아가며 수행되는 것
   - 멀티 태스킹 환경에서 프로세스가 할당 받은 시간이 종료되어 프로세스가 사용하던 CPU를 다른 프로세스가 사용할 수 있도록 재배정 할 때 발생
2. 인터럽트 핸들링
   - CPU가 프로그램을 실행하고 있을 때, 입출력 하드웨어 등의 장치나 또는 예외상황이 발생하여 처리가 필요한 경우 CPU에게 알려 처리할 수 있도록 하는 것
   - 인터럽트 종류
     - I/O request : 입출력 요청
     - time slice expired : CPU 사용시간 만료
     - fork a child : 자식 프로세스를 만듦
     - wait for an interrupt : 인터럽트 처리를 기다림
3. (유저모드 <-> 커널모드 전환)
   - 모드 전환은 그 자체로 Context Switching은 아니지만 운영체제에 따라 발생 가능

<br>

<br>

# 스케줄러(Scheduler)

- **프로세스들은 자신이 종료될 때까지 수많은 큐를 돌아다님**
- 운영체제는 큐 안에 있는 프로세스 중 하나를 선택해야 하며, 이러한 일을 **스케줄러**가 담당

<br>

### 큐(Queue)의 종류

1. Job Queue : 현재 시스템 내에 있는 모든 프로세스의 집합
2. Ready Queue : 현재 메모리 내에 있으면서 CPU를 할당받아 실행되기를 기다리는 프로세스의 집합
3. Device Queue : Deviece I/O 작업을 대기하고 있는 프로세스의 집합

<br>

### 스케쥴러의 종류



![](https://t1.daumcdn.net/cfile/tistory/27033450580366160E?download)



1. **장기 스케줄러(Long-term scheduler or job scheduler)**

- 메모리는 한정되어 있는데 많은 프로세스들이 한꺼번에 메모리에 올라올 경우, 대용량 메모리(디스크)에 임시로 저장됨. 이 디스크 내의 저장되어 있는 프로세스 중 어떤 순서로 프로세스를 메모리에 적재할지 결정
- **메모리와 디스크 사이의 스케줄링을 담당**, 호출되는 빈도가 적음
- 디스크와 같은 저장 장치에 작업들을 저장해 놓고 필요할 때 실행할 작업을 Job Queue에서 꺼내 Ready Queue를 통해서 메인 메모리에 적재
- **프로세스의 상태**
  - new -> ready

<br>

2. **단기 스케줄러(Short-term scheduler or CPU scheduler)**

- **CPU와 메모리 사이의 스케줄링을 담당**, 장기 스케줄러에 비해 많이 호출됨
- 메모리에 있는 프로세스 중 하나를 선택해서 CPU를 할당
- **즉, Ready Queue에 존재하는 프로세스 중 어떤 프로세스를 running 시킬지 결정**
- Ready Queue에 있는 프로세스 중 **먼저 도착한 프로세스에게 CPU 할당**
- **프로세스의 상태**
  - ready -> running -> waiting -> ready

<br>

3. **중기 스케줄러(Medium-term scheduler or Swapper)**

- 시분할 시스템에서 추가로 사용하며, 메모리에 대한 가중을 완화시켜주기 위해 사용
- CPU를 차지하기 위한 경쟁이 심해질 때, 우선순위가 낮은 프로세스들을 잠시 제거한 뒤, 나중에 경쟁이 완화되었을 때 다시 디스크에서 메모리로 불러와 중단되었던 지점부터 실행(**Swapping)**
- 즉, 프로세스들이 서로 CPU를 차지하려고 경쟁이 심해지면 Swapping 기법을 활용하여 메모리를 관리함으로써 너무 많은 프로그램이 동시에 올라가는 것을 조절
- **프로세스의 상태**
  - ready -> suspended

<br>

***swap out : 메모리에서 디스크로 잠시 나가는 상태***

***swap in : 디스크에서 메모리로 다시 들어오는 상태***

***suspended***

- 외부적인 이유로 프로세스의 수행이 정지된 상태로 메모리에서 내려간 상태,
- 프로세스 전부 디스크로 swap out
- Blocked 상태는 다른 I/O 작업을 기다리는 상태이므로 스스로 ready queue로 돌아갈 수 있지만, **외부적인 이유이기 때문에 suspended 상태는 스스로 돌아갈 수 없음**

<br>

<br>

# CPU 스케줄링

- CPU가 하나의 프로세스 작업이 끝나면 다음 프로세스 작업을 수행해야 함
- 실행 준비가 된 프로세스 중에서 하나를 선택해 CPU를 할당하는 것
- 상황에 맞게 CPU를 어떤 프로세스에 배정하여 효율적으로 처리하는가가 관건
- 스케줄링 대상은 **Ready Queue**에 있는 프로세스
- **CPU Scheduling은 프로세스가 아래와 같은 상황일 때 발생**
  - running -> ready : 인터럽트 발생
  - waitiing -> ready : I/O 완료
  - ready -> running : 단기 스케줄링
  - running -> waiting : I/O 요청, wait
  - terminated : 종료 시

<br><br>

### Preemptive vs Non-Preemptive

1. Preemptive : 선점 

- 프로세스가 CPU를 점유하고 있는 동안 I/O, 인터럽트가 발생하지 않았음에도 다른 프로세스가 해당 CPU를 강제로 점유 가능
- **프로세스가 정상적으로 수행중인 동안, 다른 프로세스가 CPU를 강제로 점유하여 실행**

2. Non-Premmptive : 비선점

- 한 프로세스가 CPU를 점유했다면, **I/O 나 인터럽트 발생 또는 프로세스가 종료될 때 까지 다른 프로세스가 CPU를 점유하지 못하는 것**

<br>

***선점형 스케줄링***

***SRTF, Round Robin, Priority Scheduling, Multi-level Queue, Multi-level feedback Queue 등***

<br>

***비선점형 스케줄링***

***FCFS(FIFO), SJF, Priority Scheduling, HRRN 등***

<br><br>

### 선점형 스케쥴링

: ***SRTF, Round Robin, Priority Scheduling, Multi-level Queue, Multi-level feedback Queue 등***

<br>

1. SRTF(Shortest Remaining Time First)
   - 특징 
     - 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어짐
     - 현재 수행중인 프로세스의 남은 burst time 보다 짧은 CPU burst time(CPU 사용시간)을 가지는 새로운 프로세스가 도착하면 CPU를 뺏김
   - 장점
     - 최적
     - 주어진 프로세스 집합에 대해 ***최소 평균 대시시간을 제공***
   - 단점
     - **starvation** : 특정 프로세스의 우선순위가 낮아서 원하는 자원을 계속 할당받지 못함, 즉 불공정
     - 새로운 프로세스가 도달할 때마다 스케줄링을 다시하기 때문에 CPU burst time을 측정할 수 없음

2. Round Robin

   - 특징 
     - 각 프로세스는 동일한 할당 시간(time quantum = time slice)를 갖음
     - 할당 시간동안 수행하고 할당 시간이 지나면 프로세스는 ready queue의 제일 뒤로 감
     - 한 프로세스가 종료되기 전에 할당시간이 끝나면 다른 프로세스에게 CPU를 넘겨주기 때문에 **선점형 스케줄링의 대표적 예시**
     - 프로세스가 기다리는 시간이 CPU를 사용할 만큼 증가하기에 공정한 스케줄링
     
   - 장점
     - CPU 사용시간이 랜덤한 프로세스들이 섞여있을 경우에 효율적
     - Response time이 빨라짐 : n 개의 프로세스가 ready queue 에 있고 할당시간이 q(time quantum)인 경우 각 프로세스는 q 단위로 CPU 시간의 1/n 을 얻는다. **즉, 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않음**
     
   - 성능
     - 할당 시간을 높게 설정 : FIFO
     - 할당 시간을 낮게 설정 : 스레드간에 Context Switching 하는 데 모든 시간을 소비하여 오버헤드 발생 (프로세스가 자주 바뀌므로)
     
   - ```
     time slice = 20이고, 작업 완료시 필요한 시간이 각각
     P1 = 53, P2 = 17, P3 = 68, P4 = 24 일 때 진행 과정
     완료 순서 : P2, P4, P1, P3
     ```

   - ![](https://user-images.githubusercontent.com/21440957/66187500-e1073a00-e6bf-11e9-869e-5300427b8b5e.png)

3. Priority Scheduling

   - 특징 

     - 우선순위가 가장 높은 프로세스부터 할당하는 기법으로 ***작은 숫자가 우선순위가 높음***
     - **선점, 비선점 모두 가능**
       - 선점 : 더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU를 선점
       - 비선점 : 더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head에 넣음

   - 단점

     - starvation : 특정 프로세스의 우선순위가 낮아서 원하는 자원을 계속 할당받지 못함, 즉 불공정

   - 해결책

     - Aging :  ready queue에서 기다리는 동안 일정 시간이 지나면 우선 순위를 일정량 높여주는 것. 그러면 우선순위가 매우 낮은 프로세스라 하더라도, 기다리는 시간이 길어질수록 우선순위도 계속 높아지므로 수행될 가능성이 커짐

   - ![1](https://blog.kakaocdn.net/dn/cd8NKk/btquvkjkhgj/macQZjvYxlKHc1yMXeCozk/img.png)

   - ```
     Average Waiting Time(AWT) : 0 + 6 + 16 + 18 + 1 / 5 = 8.2msec
     ```

4. Multi-level Queue(다중 레벨 큐) 스케줄링

   - **Ready Queue를 여러 개로 분할**해 관리하는 스케줄링 방법
   - 프로세스를 그룹으로 나누어, 각 그룹에 따라 Ready Queue를 여러 개 두며, 각 큐마다 다른 규칙을 지정(우선순위, CPU 할당시간 등)
   - 프로세스들의 CPU를 기다리기 위해 한 줄로 서는 게 아니라 여러 줄로 섬
   - ![](https://user-images.githubusercontent.com/34755287/53879673-5e979880-4052-11e9-9f9b-e8bfec7c9be6.png)

5. Multi-level feedback Queue(다중 레벨 피드백 큐) 스케줄링

   - 기본 개념은 Multi-level Queue와 동일하나, 프로세스가 하나의 큐에서 다른 큐로 이동 가능하다는 점이 다름
   - **큐 사이에도 우선순위를 부여하는 스케줄링 기법**
   - ![](https://user-images.githubusercontent.com/34755287/53879675-5f302f00-4052-11e9-86a2-c02ee03bac64.png)
   - 위 그림에서 모든 프로세스는 가장 위의 큐에서 CPU의 점유를 대기. 이 상태로 진행하다가 이 큐에서 기다리는 시간이 너무 오래 걸린다면 **아래의 큐로 프로세스를 옮김**
   - 만약, 우선순위 순으로 큐를 사용하는 상황에서 우선순위가 낮은 아래의 큐에 있는 프로세스에서 starvation 상태가 발생하면 이를 우선순위가 높은 위나 아래의 큐로 옮길 수 있음

<br><br>

### 비선점형 스케줄링

: **FCFS(FIFO), SJF, Priority Scheduling 등**

<br>

1. FCFS(First Come First Served) = FIFO(First In First Out)

   - 특징
     - 가장 간단한 비선점 스케줄링 기법
     - **Ready Queue에 도착한 순서대로 실행**
     - 일단 CPU를 할당받으면 CPU 할당 시간이 완료될 때까지 CPU를 반환하지 않으며, 할당되었던 CPU가 반환될 때만 스케줄링이 일어남

   - 장점

     - 구현이 간단

   - 단점

     - Convoy Effect 발생 : 소요 시간이 긴 프로세스가 짧은 프로세스보다 먼저 도착해서 뒤에 프로세스들이 오래 기다려야 하는 현상
     - 늦게 온 작업에게 불공평 (최악의 경우 : 오래 걸리는 프로세스가 먼저 도착)

   - ![](https://blog.kakaocdn.net/dn/x4n0r/btquuKbpwZF/Hn15OQvNtpmqcLjGhMomPK/img.png)

   - ```
     Average Waiting Time = 0 + 24 + 27 / 3 = 17msec
     ```

   - 프로세스가 들어온 순서가 P3, P2, P1 인 경우

   - ```
     Average Waiting Time = 6 + 3 + 0 / 3 = 3msec
     ```

   - **즉, 들어온 순서로 수행한다고 해서 반드시 효율적인 것은 아님**

2. SJF(Shortest-Job-First)

   - 특징
     - 도착 순서와 상관없이, CPU 점유 시간이 가장 짧은 프로세스에 CPU를 먼저 할당

     - **선점, 비선점 모두 가능**

       - 비선점 

       - ![](https://blog.kakaocdn.net/dn/xfVOK/btquwmHrtlS/Mb9stKxMT0HSk3S6cg4xCK/img.png)

       - ```
         Average Waiting Time = 0 + 3 + 9 + 16 / 4 = 7msec
         ```

   - 문제점

     - starvation : 점유 시간이 긴 프로세스가 요구 시간이 짧은 프로세스에게 항상 양보되어 점유 시간이 긴 프로세스는 영원히 CPU 할당 불가
     - 가장 효율적인 CPU 스케줄링 방법 같지만, 매우 **비현실적**. 왜냐하면 컴퓨터 환경에서는 프로세스의 CPU 점유시간을 알 수 없음. 점유 시간을 알려면 실제로 수행하여 측정하는 수 밖에 없지만 이는 오버헤드가 매우 큰 작업

   <br>

   <br>

   # 동기화 문제

   

   

   
