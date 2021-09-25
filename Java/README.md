# int vs Integer

### int

- primitive(기본형) 자료형
- ***산술 연산이 가능하며, null 값을 가질 수 없음***

<br>

### Integer

- Wrapper 클래스(객체)
- ***Unboxing을 하지 않으면 산술 연산이 불가능하지만, null 값을 가질 수 있음***
- Collection, null 값이 필요한 경우 사용

<br>

```java
// boxing : 기본형을 참조형으로 변환
// unboxing : 참조형을 기본형으로 변환

Integer a = new Integer(123);
int a2 = (int)a; // unboxing    
Integer b = (Integer)456; // boxing 
```

<br>

# Interface vs Abstract

### Interface

- 일종의 추상 클래스
- 추상화의 정도가 높기 때문에, 일반 메소드나 멤버 변수를 가질 수 없고 오직 **추상메소드와 상수만을 멤버로 가질 수 있음**
- **인터페이스 자체만으로 새로운 인스턴스(객체)를 생성할 수 없음**
- 사용 이유
  - 완벽한 추상화를 이루기 위해
  - 다중 상속
  - 다형성

<br>

### Abstract

- 상속을 강제하는 일종의 규제
- 일반적인 추상화 및 상속에 초점을 둠
  - 예를 들어 냉장고, TV, 커피머신 등의 클래스를 만들어야 할 일이 있을 때, 가전제품이라는 추상클래스로 추상화 시켜서 사용하면 좋음
  - 가전제품은 **공통적으로 ON, OFF, 전기소모 등 사용되는 메소드들을 적고**, **구체적인 가전제품별로 별도의 동작(메소드)을 나눠서 구현**
  - 상속 받아서 기능을 확장시키는 목적으로 사용

<BR>

#### 추상 메소드

- 메소드의 정의만 되어있는 **비어있는 메소드**
- body가 있는 메소드는 abstract 키워드를 가질 수 없음

```java
public abstract in show(); // 가능

// public abstract int show(){
//	System.out.println("hello"); 불가능
//}
```

<br>

#### 추상 클래스

- 추상 메소드를 **<u>하나라도 포함하고 있는 클래스</u>는 추상 클래스가 됨**
- **추상 클래스만으로 새로운 인스턴스(객체)를 생성할 수 없음**
- 멤버 변수와 구현된 메소드가 존재 가능
- 다중 상속 불가

<br>

# Collection

다수의 Data를 다루는 데 표준화된 클래스들을 제공해줌으로써, DataStructure를 직접 구현하지 않고 편하게 사용하기 위함

또한, 배열과 다르게 ***객체를 보관하기 위한 공간을 미리 정하지 않아도 되므로 상황에 따라 객체의 수를 동적으로 정할 수 있음***. 이는 프로그램의 공간적인 효율성 또한 높여줌

- List  
  - 대표적으로 ArrayList, LinkedList가 존재
  - 기존에 있던 Vector를 개선
- Map
  - 대표적으로 HashMap이 존재
  - key-value의 구조로 이루어져 있으며, **key를 기준으로 중복된 값을 저장하지 않으며, 순서를 보장하지 않음**
  - key에 대해서 순서를 보장하기 위해서는 LinkedHashMap을 사용
- Set
  - 대표적으로 HashSet이 존재
  - **value에 대해서 중복된 값을 저장하지 않으며, 순서를 보장하지 않음**
  - 순서를 보장하기 위해서는 LinkedHashSet을 사용
- Stack, Queue
  - Stack 객체는 new 키워드로 사용 가능
  - Queue는 JDK 1.5부터 LinkedList에 new 키워드를 적용하여 사용할 수 있음

<br>

# Hash 관련

- 모두 Collection Framework에 속함, 기본적으로 Collection Framework는 Set, List, Queue 인터페이스로 나뉘어 짐
- Set : 객체를 받지만, ***중복되는 값은 허용하지 않음(순서가 없음)***
- List : 인덱싱하여 ***중복을 허용***
- Queue : 선입선출(FCFS, FIFO) 알고리즘을 기반으로 함

<br>

### HashSet

- Set 인터페이스를 구현한 것으로 중복을 허용하지 않음
- 들어가는 객체들은 반드시 equals()와 hashCode() 메소드를 구현해야 하는데, 이 메소드들을 가지고 HashSet에 들어갈 때, 중복된 객체가 있는지 여부를 체크함

<br>

### HashMap

- Map 인터페이스를 구현한 것으로, **Key-Value 형태의 데이터를 저장**
- 중복된 Key 값은 허용하지 않으나, 중복된 값의 저장은 허용 (null value, null key를 허용)
- HashMap : 집어 넣은 **순서를 유지하지 않음**
- TreeMap : 내부적으로 [Red-Black Tree](https://zeddios.tistory.com/237)로 저장되며, Key 값을 기준으로 알파벳 순서대로 정렬
- LinkedHashMap : 집어 넣은 **순서를 유지**

<BR>

#### ***HashSet vs HashMap***

***HashSet***

- Set 인터페이스를 구현
- **객체만 저장 가능**
- 들어가는 객체를 이용하여 hashCode를 생성하고, equals() 메소드를 이용해 hashCode를 비교해서 중복된 객체가 있는지 체크
- ***equals() 메소드는 중복된 객체가 있으면 True, 없다면 False***
- ***HashMap에 비해서 느림***

<br>

***HashMap***

- Map 인터페이스를 구현
- **데이터를 Key-Value 형식으로 저장**
- hashCode 값은 key value를 이용하여 생성
- ***unique key를 이용하여 데이터에 접근하기에 HashSet에 비해 빠름***

<br>

#### ***HashTable vs HashMap***

- Map 인터페이스를 구현한 클래스
- key, value를 이용하여 값을 저장하는 구조

<br>

***HashTable***

- **동기화를 지원하므로 멀티 스레드 환경에서 사용 가능**
- Key, Value의 **Null을 허용하지 않음**
- put, get과 같은 주요 메소드에 synchronized 키워드가 선언되어 있음
- 동기화 처리 비용이 있기에 속도가 느림
- **Enumeration을 반환**
- Enumeration은 Collection 프레임워크 이전에 사용되던 인터페이스로 Iterator의 사용을 권장

<br>

***HashMap***

- **동기화를 지원하지 않으므로 멀티 스레드 환경에는 적합하지 않음**
- **Key, Value의 Null을 허용**
- 주요 메소드에 synchronized 키워드가 선언되어 있지 않음
- HashTable에 비해 속도가 빠름
- **저장된 요소들의 순회를 위해 Iterator를 반환**

<br>

# == vs equals()

### ==

- 비교를 위한 **연산자**
- 비교하고자 하는 대상의 **주소값**을 비교

### equals()

- 비교를 위한 **메소드**
- 비교하고자 하는 대상의 **내용 자체**를 비교
- 객체끼리 내용을 비교

```java
String a = "a";
String b = a;
String c = new String("a");

// 주소값을 비교
a == b; // true
a == c; // false

// 내용을 비교
a.equals(b); // true
a.equals(c); // true
```

<br>

#### equals() 메소드 동작 원리

```java
public boolean equals()(Object anObject){
  if(this == anObject) return true;
  
  if(anObject instanceof String){
    String anotherString = (String) anObject;
    int n = value.length;
    if(n == anohterString.value.length){
      char v1[] = value;
      char v2[] = anotherString.value;
      
      int i = 0;
      while(n-- !=0){
        if(v1[i] != v2[i]) return false;
        
        i++;
      }
      return true;
    }
  }
  return false;
}
```

1. 같은 객체인지 비교 후, 같은 객체라면 같은 값을 가지고 있기 때문에 true를 반환하며 아래 문장은 수행되지 않음
2. 다음으로 인자로 들어온 anObject가 String 타입인지 확인하고, 조건을 만족하면 해당 객체를 String 타입으로 형 변환
3. char[] 배열로 변환한 뒤, 문자를 앞에서부터 하나식 비교. 한 개의 문자라도 다르다면 false를 반환하고, 모두 같다면 true를 반환

<br>

# Call by Value vs Call by Reference

#### Java는 **Call by Value**

- Primitive Type : Call by Value (int, short, char, boolean 등)
  - 함수의 인자로 전달되는 타입이 Primitive인 경우 값을 넘기게 되어있음. 이 경우 메모리에는 함수를 위한 별도의 공간이 생성되고, **이는 함수 종료시 사라짐**. 따라서 함수 안에서 해당 인자의 값을 변경하더라도 원본 값은 바뀌지 않는 특징을 가짐

```java
public class Test {
    public static void main(String[] args) {
        int n = 10;
        System.out.println(n);
        test(10);
        System.out.println(n);
        // 값이 바뀌지 않는다는 걸 볼 수 있다. 
    }

    public static void test(int n) {
        n -= 5;
        System.out.println(n);
    }
}
// 결과
10
5
10
```



- **Reference Type : Call by reference (array, 참조 타입 등)**
  - Reference type인 경우, 변수가 가지는 값이 주소 값이므로 Call by reference에 의해 주소 값이 전달 됨. 따라서 함수 안에서 해당 인자의 값을 변경하게 되면 원본 값도 바뀌는 특징을 가짐

```java
public class Test {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3};
        for (int num : arr) System.out.print(num + " ");
        System.out.println();
        test(arr);

        for (int num : arr) System.out.print(num + " ");
    }

    // 참조형의 경우, 주소값이 전달되므로 값을 변경하면 원본도 영향을 받는다.
    public static void test(int[] a) {
        for (int i = 0; i < a.length; i++) {
            a[i] *= 10;
        }
    }
}
// 결과
1 2 3 
10 20 30 
```

<br>

# Garbage Collection

1. stop-the-world
   - GC를 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것
   - **stop-the-world가 발생하면 GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춤**
   - ***어떤 GC 알고리즘을 사용하더라도 stop-the-world 발생***
   - 대게 GC 튜닝이란 stop-the-world 시간을 줄이는 것

<br>

2. **Minor GC**  

![](https://d2.naver.com/content/images/2015/06/helloworld-1329-3.png)

- 새로 생성된 대부분의 객체는 Eden 영역에 위치
- **Eden 영역이 꽉 차게 되면 GC 발생**. 그 이후, 살아남은 객체는 Survivor 영역으로 이동
- 이 과정을 반복하다가 계속해서 살아남은 객체는 일정 시간 참조되고 있다는 뜻이므로 Old 영역으로 이동

<br>

3. **Major GC (Full GC)**

- Old 영역에 있는 모든 객체들을 검사하여 참조되고 있지 않은 객체들을 한꺼번에 삭제
- 시간이 오래 걸림
- GC 작업 완료 후, 중단했던 작업을 다시 시작

<BR>

***JVM의 메모리 공간은 매우 많은 객체가 생성되는 Young Generation과 Minor GC가 발생하고도 살아남은 객체가 모이는 Old로 나뉘었고,각 Minor GC와 Major GC가 발생한다.***

<BR>

#### GC는 어떤 원리로 소멸시킬 대상을 선정하는가

![](https://user-images.githubusercontent.com/33534771/83470789-0605b400-a4be-11ea-84e6-6044596242d3.png)

- GC는 힙 내의 객체 중에서 Garbage를 찾아내고, 찾아낸 Garbage를 처리해서 힙의 메모리를 회수
- **참조되고 있지 않은 객체를 Garbage**라고 하며, 객체가 Garbage인지 아닌지 판단하기 위해서는 **Reachability**라는 개념을 사용
- 어떤 힙 영역에 할당된 객체가 유효한 참조가 있으면 Reachability, 없다면 UnReachability
- 하나의 객체는 다른 객체를 참조하고, 다른 객체는 또 다른 객체를 참조할수 있기 때문에 ***참조 사슬이 형성됨***. 이 참조 사슬 중 ***최초의 참조한 것을 Root Set***
- 유효한 최초의 참조가 이루어지지 않은 객체들은 Unreachable Objects로 판단하며 GC에 의해 수거
- **빈번한 GC의 실행은 시스템에 부담이 되기 때문에 바로 소멸되는 것은 아님**. 성능에 영향을 미치지 않도록 GC 실행 타이밍은 별도의 알고리즘을 기반으로 계산이 되며, 이 계산 결과를 바탕으로 GC를 수행

[참고1](https://d2.naver.com/helloworld/1329),[참고2](https://velog.io/@agugu95/%EC%9E%90%EB%B0%94-GC-Garbage-Collection)

<BR>

---------------------------------------------

# JVM (Java Virtual Machine)

- 스택 기반 가상 머신
- Java 애플리케이션을 클래스 로더를 통해 읽어들여 Java API와 함께 실행하는 것
- Java와 OS 사이에서 중개자 역할을 수행하여, Java가 OS에 구애받지 않고 재사용이 가능하게 해줌
- **메모리 관리, GC를 통해 자원관리 를 수행** => 한정된 메모리를 효율적으로 사용하여 최고의 성능을 내기 위함
- Java 바이트 코드를 실행할 수 있는 주체

<BR>

### Java 프로그램 실행 과정

1. 프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로 하는 메모리를 할당받음. JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리
2. Java 컴파일러 (javac)가 Java 소스 코드를 읽어들여 Java 바이트 코드 (.class) 로 변환시킴
3. Class Loader를 통해 class 파일들을 JVM으로 로딩
4. 로딩된 class 파일들은 Execution Engine을 통해 해석
5. 해석된 바이트 코드는 Runtime Data Area에 배치되어 실질적인 수행이 이루어 짐

***이러한 실행 과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC 같은 관리 작업을 수행***

<BR>

### 각각의 역할

![](https://user-images.githubusercontent.com/33534771/83471568-f7200100-a4bf-11ea-810f-3ea08018317f.png)

#### Class Loader (클래스 로더)

- Runtime(클래스를 처음으로 참조할 때) 시, JVM 내로 클래스(.class 파일)를 로드하고 링크를 통해 배치하는 작업을 수행 
- JVM 내의 Runtime Data Area에 바이트 코드를 배치시킴
- ***사용하지 않는 클래스들을 메모리에서 삭제***
- 동적 로드를 담당

<br>

#### Execution Engine (실행 엔진)

- 클래스를 실행시키는 역할
- Runtime Data Aread에 배치된 바이트 코드를 실행시킴
- Java 바이트 코드는 비교적 인간이 보기 편한 형태로 기술된 것. 이를 JVM 내부에서 기계가 실행할 수 있는 형태로 변경하는 역할
- Java 바이트 코드를 명령어 단위로 읽어서 실행
- 2가지 방식이 존재
  - 최초의 JVM은 인터프리터 방식이었기 때문에 속도가 느린 단점이 존재, JLT 컴파일러 방식을 통해 이 점을 보완
  - Interpreter(인터프리터)
    - Java 바이트 코드를 **명령어 단위로 읽어서 실행**
    - **한 줄씩 실행하기 때문에 느림**
  - JIT (Just-In-Time) Compiler
    - 인터프리터 방식의 단점을 보완하기 위해 등장
    - 인터프리터 방식으로 실행하다가 **적절한 시점에 바이트 코드 전체를 컴파일하여 네이티브 코드로 변경하고, 이후에는 더 이상 인터프리팅하지 않고 네이티브 코드로 직접 실행하는 방식**
    - **네이티브 코드는 캐시에 보관**하기 때문에 한 번 컴파일된 코드는 빠르게 수행
    - 한 번만 실행되는 코드라면 인터프리팅하는 것이 유리
    - ***이처럼 해당 메소드가 얼마나 자주 수행되는지 체크하고, 일정 정도를 넘을 때만 컴파일을 수행하는게 유리***

<br>

#### Garbage Collector

- GC를 수행하는 모듈 존재

<BR>

#### Runtime Data Area

- **JVM이 프로그램을 수행하기 위해 OS로부터 할당받은 메모리 공간**
- 이 공간은 용도에 따라 여러 영역으로 나누어 관리

![](https://user-images.githubusercontent.com/33534771/83472428-2fc0da00-a4c2-11ea-90a9-dac474fada4b.png)

1. PC 레지스터
   - Thread가 시작될 때, 각각의 Thread 별로 생성되는 공간으로 ***현재 수행 중인 JVM <u>명령어 주소</u>를 가짐***
2. JVM 스택 영역
   - 프로그램의 실행 과정에서 **임시로 할당되었다가 메소드를 빠져나가면 바로 소멸되는 특성의 데이터를 저장하기 위한 영역**
   - 메소드의 매개 변수, 지역 변수 등 메소드의 정보를 저장
3. Native Method Stack
   - Java외의 언어로 작성된 네이티브 코드를 위한 영역
   - 바이트 코드가 아닌 **실제 실행할 수 있는 기계어로 작성된 프로그램을 실행시키는 영역**
4. Method Area (Class Area, Static Area)
   - 클래스 정보를 처음 메모리 공간에 올릴 때, 초기화 되는 대상을 저장하기 위한 메모리 공간
   - **모든 쓰레드가 공유하는 메모리 영역**
   - 클래스, 인터페이스, 메소드, 필드, Static 변수 등의 **바이트 코드를 보관**
   - Runtime Constant Pool 이라는 것이 존재하며, 이는 별도의 관리 영역으로 상수 자료형을 저장하여 참조하고 중복을 막는 역할
   - **Java 7** 부터 String Constant Pool은 Heap 영역으로 변경되어 GC의 관리 대상이 되었음 => **모든 문자열도 GC의 대상이 됨**

5. Heap (힙 영역)

   - **객체와 배열을 저장하는 가상 메모리 공간**
   - **런타임시 동적으로 할당하여 사용하는 영역**
   - **GC의 관리 대상에 포함**
   - <img src="https://user-images.githubusercontent.com/33534771/83472881-3f8cee00-a4c3-11ea-942c-9b7aa0f4ea04.png" style="zoom:200%;" />
   
     - New/Young 영역
       - Eden : 객체들이 최초로 **생성되는 공간**
       - Survivor : Eden에서 참조되는 객체들이 **저장되는 공간**
     - Old 영역
       - New 영역에서 일정 시간 참조되고 **살아남은 객체들이 저장되는 공간**
       - Eden 영역에서 인스턴스(객체)가 가득차게 되면 첫 번째 GC가 발생 (**Minor GC)**
       - Eden 영역에 있는 값들을 Survivor 1 영역에 복사하고, **이 영역을 제외한 나머지 영역의 객체를 삭제**
       - **Eden 영역에서 GC가 한 번 발생한 후, 살아남은 객체는 Survivor 영역으로 이동. 이 과정을 반복하다가 살아남은 객체는 Old 영역으로 이동**
     - Permanent 영역
       - 생성된 객체들의 **주소값이 저장되는 공간**
       - 리플렉션을 사용하여 동적으로 클래스가 로딩되는 경우 사용
       - Old 영역에서 살아남은 객체가 영원히 남아있는 곳이 아님
       - 이 영역에서 발생하는 GC는 Major GC의 횟수에 포함

<BR>

# Thread

### 멀티 태스킹

- 두 가지 이상의 작업을 동시에 하는 것
- 실제로는 동시에 처리될 수 있는 프로레스의 개수가 CPU 코어의 개수와 동일한데, 이보다 많은 개수의 프로세스가 존재하기 때문에 모두 함께 동시에 처리될 수 없음
- ***각 코어들은 아주 짧은 시간 동안 여러 프로세스를 번갈아가며 처리하는 방식을 통해 동시에 동작하는 것처럼 보이게 할 뿐***

<BR>

### 멀티 스레딩

- 하나의 프로세스 안에서 여러 개의 스레드(하나의 작업 단위)가 동시에 작업을 수행하는 것

<BR>

### 스레드 구현 방법

1. Runnable 인터페이스 구현

```java
public class MyThread implements Runnable{
    @Override
    public void run(){
        //수행 코드
    }
}

public static void main(String[] args){
    Runnable runnable = new MyThread();
    Thread t = new Thread(runnable, "mythread");
}
```

- Runnable 인터페이스를 구현하므로 다른 클래스를 상속받을 수 있음
- run() 메소드를 오버라이드 하면 됨
- 다만, start() 메소드가 없기 때문에 Runnable 인터페이스를 구현할 클래스의 객체를 만들어 Thread를 생성할 때, 생성자의 매개변수로 넘겨주고 스레드 객체의 start() 메소드를 수행

<br>

2. Thread 클래스 상속

```java
public class MyThread extends Thread{
    public void run(){
        //수행 코드
    }
}
```

- Thread 클래스를 상속받으면 다른 클래스를 상속받지 못함(**다중 상속 불가능 - Java**)
- run() 메소드를 직접 구현
- Thread 클래스를 상속받으면 스레드 클래스의 메소드를 바로 사용할 수 있지만, Runnable 구현의 경우 Thread 클래스의 static 메소드인 currentThread()를 호출해 현재 스레드에 대한 참조를 얻어와야만 호출이 가능

<br>

### 스레드의 실행

- **run() 호출이 아닌 start() 호출로 실행**
- Java에는 Call Stack이 존재. 이 영역이 실질적인 명령어들을 담고 있는 메모리로, 하나씩 꺼내서 실행시키는 역할
- 만약 동시에 두 가지 작업을 한다면, 두 개 이상의 Call Stack이 필요. **스레드를 이용한다는 건 JVM이 다수의 Call Stack을 번갈아가며 일처리를 하고 사용자에게는 동시에 작업을 하는 것처럼 보여주는 것**

- 즉, run() 메소드를 이용한다는 것은 Call Stack 하나만 이용하는 것으로 스레드 활용이 아님
- **start() 메소드를 호출하면 JVM은 알아서 스레드를 위한 콜 스택을 새롭게 만들어주고 context switching을 통해 스레드답게 동작하도록 해줌**
- start()는 스레드가 작업을 실행하는 데 필요한 Call Stack을 생성한 다음, ***run()을 호출해서 그 Stack 안에 run()을 저장할 수 있도록 해줌***

<BR>

# String

### 생성 방식

1. **new** 연산자를 이용한 방식
2. 리터럴을 이용한 방식

**new를 통해 String 객체를 생성하면 Heap 영역에 존재**

**리터럴을 이용할 경우, String Constnat Pool 영역에 존재**

```java
public class StringMemory{
    public static void main(String[] args){
        String literal = "money";
        String obj = new String("money");
        
        literal == obj; // false
        literal.equals(obj); // true
    }
}
```

- == 연산 결과는 false : **== 연산자는 주소값을 비교**하므로, 일반 객체처럼 Heap 영역에 생성된 obj (String 객체)와, String Constant Pool (***Runtime Data Area -> Method Area -> Runtime Constant Pool***)에 저장된 literal의 주소값은 다름
-  equals() 메소드의 결과는 true : **equals() 메소드는 내용을 비교**하므로, 같은 문자열에 대해서는 true를 반환

[참고](https://sabarada.tistory.com/137)

