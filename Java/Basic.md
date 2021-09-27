# 객체지향 프로그래밍

- OOP (Object Oriented Programming)
- 프로그래밍에서 필요한 데이터를 추상화시켜 상태와 행위를 가진 객체를 만들고, 그 객체들 간의 유기적인 상호작용을 통해 로직을 구성하는 프로그래밍 방법 

### 장점

- 코드의 재사용성이 높음 : 누군가가 만든 클래스를 가져와 사용할 수 있고, 상속을 통해서 확장할 수 있음
- 유지보수가 쉬움 : 수정해야 할 부분이 클래스 내부에 멤버 변수 혹은 메소드로 존재하기 때문에 해당 부분만 수정하면 됨
- 대형 프로젝트에 적합 : 클래스 단위로 모듈화시켜서 개발할 수 있으므로 업무 분담이 쉬움

### 단점

- 처리 속도가 상대적으로 느림 : JVM 로딩, 바이트코드를 기계어로 변역, GC에 의한 실행 지연 등
- 객체가 많으면 용량이 커짐 : 객체는 메모리에 저장되므로
- 설계 시 많은 노력과 시간이 필요

<BR>

### 특징

1. 추상화
   - ***불필요한 정보는 숨기고, 필요한 정보만을 표현함으로써 공통의 속성이나 기능을 묶어 이름을 붙이는 것***
2. 캡슐화
   - 속성과 기능을 정의하는 멤버 변수와 메소드를 클래스라는 캡슐에 넣는 것
   - 즉, 관련된 속성(변수)과 기능(메소드)을 한 곳에 모으고 뷴류하기 때문에 재활용이 원활
   - 그래서 클래스에 속하지 않는 변수나 메소드는 존재 불가능
   - 목적 : 코드를 수정 없이 재활용 하는 것, 정보 은닉

3. 상속
   - 상속을 통해서 클래스를 작성하면 보다 적은 양의 코드로 새로운 클래스 작성 가능
   - 코드를 공통적으로 관리하여 코드 추가 및 변이가 용이
4. 다형성
   - 하나의 변수명, 함수명 등이 상황에 따라 다른 의미로 해석 가능
   - 즉, 오버라이딩, 오버로딩이 가능

<br>

# 기본형과 참조형의 차이

1. 기본형 (Primitive Type)
   - 변수에 값 자체를 저장하며, **stack 영역에 생성**
   - 사용하기 전에 반드시 선언되어야 하며, 초기화를 하지 않으면 자료형에 맞는 **기본 값**이 들어감
   - ***선언 즉시 사용 가능***
   - OS에 따라 자료의 길이가 변하지 않음
   - 비객체 타입이며, **Null을 가질 수 없음**
   - 정수 (byte, short, int, long), 실수 (float, double), 문자 (char), 논리 (boolean)
   - 변수를 선언한 메소드가 종료될 때 혹은 소속된 객체가 사라질 때, 소멸
   - 복사 시, 별개의 복사본이 생성되며 복사 후 원본과 복사본은 별개의 변수
   
2. 참조형 (Reference Type)
   - 기본형 8가지를 제외한 자료형
   - 메모리 상에서 객체가 존재하는 **주소를 저장하며, Heap 영역에 저장** => stack 영역에는 참조값만 존재하고 실제 값은 Heap 영역
   - 초기화를 하지 않으면 **Null 값이 기본으로 들어감**
   - 선언에 의해 참조만 생성될 뿐 ***선언 즉시 사용할 수 없음***. **반드시 new 연산자로 메모리를 할당받아 초기화 해야 함**
   - 스트링형, 클래스형, 인터페이스형, 배열형 존재
   - 참조형 끼리의 대입은 Heap 영역에 존재하는 데이터를 참조하는 **참조자가 하나 더 늘어날 뿐**, 별도의 메모리가 추가로 할당도지 않음. 그래서 **둘 중 하나를 변경하면 다른 참조자는 같은 값을 참조하기 때문에 같이 변경됨** (해결을 위해 Deep Copy 진행)
   - **더 이상 참조하는 변수가 없을 때 GC에 의해 제거**
   - 값을 필요로 할 때마다 언박싱 과정을 거쳐야 하므로 기본형과 비교해서 접근 속도가 느림

성능과 메모리에 장점이 있는 기본형을 먼저 고려해봄. 만약 Null을 다뤄야 하거나 제네릭 타입에서 사용되어야 한다면 참조형 사용

<br>

# 클래스와 인스턴스

- 클래스
  - 어떤 문제를 해결하기 위한 데이터를 만들기 위해 추상화를 거쳐 집단에 속하는 속성과 행위를 변수와 메소드로 정의한 것
- 인스턴스
  - 클래스에서 정의한 것을 토대로 실제 메모리 상에 할당된 것으로, 실제 프로그램에서 사용되는 데이터
  - 독립된 메모리 공간에 저장된 자신만의 필드를 가짐

<br>

# 변수(멤버)의 종류의 종류

```java
public class Test {
    int a; // 인스턴스 변수
    static int b; //클래스 변수
    
    void show(){
        int c; // 지역 변수
    }
}
```

```java
Test t = new Test();
t.a; // 인스턴스 변수 사용
Test.b; // 클래스 변수 사용
```

***전역변수 = 인스턴스 변수, 클래스 변수***

1. 인스턴스 변수 (non-static 변수)

   - <u>인스턴스가 생성될 때 생성 됨</u>. 따라서 인스턴스 변수를 사용하기 전에 먼저 객체를 생성
   - 객체가 사라지면 해당 변수도 사라짐
   - **독립적인 저장공간**을 가지므로 **공유되지 않으며**, **인스턴스 별로 다른 값을 가질 수 있음**
   - 따라서 각 인스턴스마다 고유의 값을 가져야 할 때 선언
   - **Heap**에 저장됨

2. 클래스 변수 (static 변수)

   - 인스턴스 생성 없이 접근할 수 있으므로 **클래스이름.클래스변수**를 통해 접근 가능
   - <u>클래스가 로딩될 때 생성</u>되어(그러므로 딱 한번만 메모리에 올라감) 종료될 때까지 유지, 종료 후 사라짐
   - 객체가 사라져도 해당 변수는 사라지지 않음

   - **해당 클래스의 모든 인스턴스가 공통된 값을 공유**
   - 따라서 한 클래스의 모든 인스턴스가 공통적인 값을 가져야 할 때 선언
   - **메소드 영역**에 저장되며, 주로 ***공유의 목적***

3. 지역 변수

   - **메소드 내에 선언되며 메소드 내에서만 사용 가능한 변수**
   - 메소드가 실행될 때, 메모리를 할당받으며 메소드가 끝나면 소멸되어 사용 불가
   - **Stack**에 저장됨

<br>

# 접근 제어 지시자

- public : 어떤 클래스에서도 접근 가능, public 메소드는 private 멤버와 프로그램 사이의 인터페이스 역할을 수행하기도 함
- protected : protected 멤버를 포함하는 클래스가 정의되어 있는 해당 패키지 내, 그리고 ***해당 클래스를 상속 받은 외부 패키지의 자식 클래스에서 접근 가능***
- private : 해당 멤버를 선언한 클래스에서만 접근이 가능. public 메소드 (getter)를 이용한다면 해당 객체의 private 한 멤버에 접근이 가능
- Default : 같은 클래스의 멤버와 해당 클래스가 정의되어 있는 ***패키지 내에서만 접근이 가능*** 

### 참고

1. private의 경우

Private 멤버나 메소드를 가지고 있는 클래스를 A라고 하자.

그리고 B라는 클래스가 A를 상속받는다. 이 경우, B 클래스는 private으로 선언된 멤버 혹은 메소드에 접근할 수 없다.

따라서 **상속을 받더라도 private한 멤버에는 접근이 불가능 하다.**

대신, public 메소드 통해 getter를 만들면 private 멤버를 사용할 수 있다.

1. protected의 경우

Protected 멤버나 메소드를 가지고 있는 클래스를 A라고 하자.

마찬가지로 B라는 클래스가 A를 상속받는다. 이 경우, B 클래스는 protected로 선언된 멤버 혹은 메소드에 접근이 가능하다. B 라는 클래스가 다른 패키지에 선언되었을지라도 A 클래스의 멤버에 접근이 가능하다.

하지만, 다른 패키지의 A 클래스를 상속받지 않은 클래스는 A 클래스의 멤버에 접근할 수 없다. 마치 private 처럼 말이다.

<br>

# 메모리 구조

![](https://user-images.githubusercontent.com/33534771/74100794-00363c80-4b76-11ea-9616-2a819e6dcb4b.png)

1. 메소드 영역
   - 클래스에 대한 정보와 함께 클래스 변수(static)가 저장되는 영역
   - JVM은 자바 프로그램에서 특정 클래스가 사용되면, 해당 클래스의 클래스 파일(*.class)을 읽어들여, 클래스에 대한 정보를 메소드 영역에 저장
2. 힙 영역
   - **모든 인스턴스 변수(멤버 변수)가 저장되는 영역**
   - **new** 키워드를 사용해 인스턴스가 생성되면, 해당 인스턴스의 정보를 힙 영역에 저장
   - ***메모리의 낮은 주소 -> 높은 주소 순으로 할당 됨***
3. 스택 영역
   - 메소드가 호출될 때, 메소드의 스택 프레임(스택 영역에 저장되는 메소드의 호출 정보)이 저장(할당)되는 영역
   - **메소드 호출 시, 메소드 호출과 관계되는 매개 변수와 지역 변수를 스택 영역에 저장**
   - 메소드 호출이 완료되면 소멸
   - 후입 선출
   - ***메모리의 높은 주소 -> 낮은 주소 순으로 할당 됨***

<br>

# 오버라이딩, 오버로딩

### 오버라이딩 (Overriding)

```java
class Woman{ //부모클래스
    public String name;
    public int age;
    
    //info 메서드
    public void info(){
        System.out.println("여자의 이름은 "+name+", 나이는 "+age+"살입니다.");
    }
    
}
 
class Job extends Woman{ //Woman클래스(부모클래스)를 상속받음  
    String job;    
    public void info() {//부모(Woman)클래스에 있는 info()메서드를 재정의
        System.out.println("여자의 직업은 "+job+"입니다.");
    }
}
 
public class OverTest { 
    public static void main(String[] args) {        
        Job job = new Job();        
        job.name = "유리";
        job.age = 30;
        job.job = "프로그래머";
        job.info();        
    } 
}
// Out : 여자의 직업은 프로그래머 입니다.
```

- 상위 클래스, 인터페이스에 존재하는 **메소드를 하위 클래스에서 <u>재정의하는 것</u>을 의미**

- 상위 클래스의 메소드는 무시하고, **자식 클래스의 메소드 기능을 사용 하는것**
- 상속 시, 상위 클래스의 private 변수를 제외한 모든 변수를 상속 받음
- 자바의 경우 오버라이딩 시 동적 바인딩

```java
class Woman{ //부모클래스
    public String name;
    public int age;
    
    //info 메서드
    public void info(){
        System.out.println("여자의 이름은 "+name+", 나이는 "+age+"살 입니다.");
    }
    
}
 
class Job extends Woman{ //Woman클래스(부모클래스)를 상속받음  
    String job;    
    public void info() {//부모(Woman)클래스에 있는 info()메서드를 재정의
        super.info(); 
        System.out.println("여자의 직업은 "+job+"입니다.");
    }
}
 
public class OverTest { 
    public static void main(String[] args) {        
        Job job = new Job();        
        job.name = "유리";
        job.age = 30;
        job.job = "프로그래머";
        job.info();        
    } 
}
// 여자의 이름은 유리, 나이는 30살 입니다. - 부모 호출
// 여자의 직업은 프로그래머 입니다. 
```

- super를 사용함으로 써 자식 클래스를 호출했을 때, 상위 클래스의 내용 또한 가져옴
- 흐름 : Job 에 info() -> Woman 에 info() -> Job 에  info() 아래 줄

<br>

### 오버로딩 (Overloading)

```java
//이름이 cat인 메서드
void a(){
    System.out.println("매개변수 없음");
}

//매개변수 int형이 2개인 cat 메서드
void a(int a, int b){
    System.out.println("매개변수 :"+a+", "+b);
}

//매개변수 String형이 한 개인 cat 메서드
void a(String c){
    System.out.println("매개변수 : "+ c);
}
```

- **같은 이름의 메소드를 여러개 가지면서 <u>매개변수의 유형과 개수가 다르도록 하는것</u>을 의미**

- **return 타입은 동일하거나 달라도 무관**
- 자바의 경우 오버로딩 시 정적 바인딩

| 구분           | 오버라이딩                             | 오버로딩        |
| -------------- | -------------------------------------- | --------------- |
| 메소드 이름    | ***상위 클래스의 메소드 이름과 동일*** | 자체적으로 동일 |
| 매개변수, 타입 | 동일                                   | 다름            |
| return 타입    | 동일                                   | 상관 없음       |

<BR>

# Abstract

### 추상 클래스

```java
abstract class Car {
    abstract void accelrate();
}
```

- 미완성된 클래스
- **추상 클래스는 미완성된 메소드인 추상 메소드를 포함**
- **새로운 클래스를 작성하는데 있어 그 바탕이 되는 부모 클래스로서의 중요한 의미를 가짐**
- 클래스 앞에 **abstract**를 붙임

<br>

### 목적

- 기존의 클래스에서 공통된 부분을 추상화하여 상속하는 클래스에게 구현을 강제화 함
- 메소드의 동작은 구현하는 **자식 클래스에게 위임**
- 상속을 통해 기능을 확장시킴
- ***공유의 목적으로 만들기도 하기 때문에***, abstract 키워드가 있는 클래스라고 모두 구현해야 하는 것은 아님

<br>

### 특징

```java
abstract class Animal {
  abstract void cry();
}

class Cat extends Animal {
  @Override
  void cry(){
    System.out.println("냐옹냐옹 ~~!");
  }
}

class Dog extends Animal {
  @Override
  void cry(){
    System.out.println("멍멍 ~~!");
  }
}

public class Test{
  public static void main(String[] args){
    // Animal animal = new Animal();
    // 추상 클래스는 자체적으로 인스턴스를 생성할 수 없다. 불완전하기 때문에.
    
    Cat cat = new Cat();
    Dog dog = new Dog();
    
    cat.cry();
    dog.cry();
    
  }
}
```

- 추상 메소드 뿐 아니라, **일반 메소드, 멤버도 포함 가능**
- 추상 메소드를 하나라도 포함호고 있다면 추상 클래스로 선언해야 함
- 동작이 정의되어 있지 않은 **추상 메소드를 포함하고 있으므로 인스턴스 생성 불가**

<br>

### 추상 메소드

- 선언부만 작성하고 구현부는 작성하지 않는 메소드이며, 앞에 abstract 키워드를 붙임
- 구현부를 작성하지 않는 이유는 메소드의 내용이 상속받은 클래스에 따라 달라질 수 있기 때문
- 사용하는 목적은 추상 메소드를 포함한 클래스를 **상속받는 자식 클래스가 반드시 추상 메소드를 구현하도록 강제하기 위함**
- **추상 클래스를 상속받은 자식 클래스는 오버라이딩을 통해 부모인 추상 클래스의 <u>추상 메소드를 모두 구현</u>해야 함**
- 만약, 자식 클래스에서 <u>추상 메소드를 하나라도 구현하지 않는다면 자식 클래스 역시 추상 클래스로 지정</u>

# Interface

### 인터페이스

```java
interface 인터페이스 이름 {
    public static final 타입 상수이름 = 값; 
    public abstract 메소드이름(매개변수 목록); // 추상 메소드
}
```

- 인터페이스는 인터페이스를 구현하는 모든 클래스에 대해 **특정한 메소드가 반드시 존재하도록 강제함**
- 인터페이스의 목적은 **구현 객체가 같은 동작을 한다는 것을 보장하는 것**
- 일종의 추상 클래스
- 그러나 ***추상 클래스보다 추상화 정도가 높아서, 추상 메소드 이외의 일반 메소드나 멤버 변수를 구성원으로 가질 수 없음***
- **오직 추상 메소드와 상수만 멤버로 가질 수 있으며**, 그 외의 요소는 허용하지 않음
- 추상 클래스를 부분적으로만 완성된 미완성 설계도라고 한다면, 인터페이스는 구현이 된 것이 아무것도 없는 기본 설계도

<br>

### 목적

- 완벽한 추상화를 이루기 위해 (메소드 구현 목적)
- 다중 상속
- 다형성

<br>

### 제약 사항

```java
interface CardGame {
  public static final int NUMBER = 4;
  
  final int DIAMOND = 3;
  static int HEART = 2;
  int CLOVER = 1;
  // 위의 상수는 모두 public static final이며, 생략된 형태이다.
  
  public abstract int getCardNumber();
  
  String getCardKind();
  
  // public 생략.
  default void getNewCard() {
    
  }
  
  // public 생략.
  static void staticMethod() {
      
  }
}
```

- 모든 멤버 변수는 public static final, 생략 가능
- 모든 메소드는 public abstract, 생략 가능
- JDK 1.8부터 인터페이스에 static 메소드와 디폴트 메소드의 추가를 허용

<br>

### 인터페이스 상속

```java
interface Fightable extends Movable, Attackable {}

interface Movable{ 
	void move(int x,int y);
}
interface Attackable{ 
	void attack(Unit u);
}
```

- **인터페이스는 인터페이스로부터만 상속 가능**
- **클래스와 달리 다중 상속 가능**
- extends 사용

<br>

### 인터페이스 구현

```java
interface Fightable {
    void move(int x, int y);
    void attack(Unit u);
}
// Fighter 클래스는 Fightable 인터페이스를 구현했다.
// 1. 추상 메소드를 모두 구현하는 경우
class Fighter implements Fightable {	
    public void move(int x, int y) { /* 내용 생략 */ }
    public void attack(Unit u) { /* 내용 생략 */ }
}

// 2. 추상 메소드를 일부만 구현하는 경우 - 클래스 앞에 abstract를 붙여야 함
abstract class Fighter implements Fightable {
    public void move(int x, int y) { /* 내용 생략 */ }
    //public abstract void attack(Unit u) // 보이지 않지만 상속의 결과로 생략되어 있는 것
}
```

- 인터페이스에 정의된 추상 메소드를 완성하는 것
- implements 사용

<br>

### 장점

- 대규모 프로젝트 개발 시, 일관되고 정형화된 개발을 위한 표준화가 가능
- 클래스의 작성과 인터페이스의 구현을 동시에 진행할 수 있으므로, 개발 시간 단축
- 클래스와 클래스 간의 관계를 인터페이스로 연결하면 클래스마다 독립적인 프로그래밍이 가능

[참고](https://jaegom.tistory.com/39)

<br>

### 클래스를 이용한 다중 상속의 문제점

```java
class Animal {
  public void cry(){
    System.out.println("짖기!");
  }
}

class Cat extends Animal {
  @Override
  public void cry(){
    System.out.println("냐옹냐옹!");
  }
}

class Dog extends Animal{
  @Override
  public void cry(){
    System.out.println("멍멍!");
  }
}

class MyPet extends Cat, Dog { ... }
// 1.

public class Test {
  public static void main(String[] args){
    MyPet pet = new MyPet();
    pet.cry();
    // 2.
  }
}
```

- 다중 상속을 허용할 경우, **메소드 출처의 모호성** 문제 발생
- 2에서 pet.cry() 호출 시, Dog 클래스의 cry() 인지, Cat 클래스의 cry() 인지 구분할 수 없음
- 이와 같은 이유로 Java에서는 다중 상속을 지원하지 않음
- 하지만 인터페이스를 이용해 다중 구현을 하게되면 위와 같은 문제 방지

```java
interface Animal {
  void cry();
}

interface Cat extends Animal {
  void cry();
}

interface Dog extends Animal {
  void cry();
}

class Pet implements Cat, Dog {
  @Override
  public void cry(){
    System.out.println("멍멍~ 냐옹냐옹~")
  }
}

public class Test{
  public static void main(String[] args){
    Pet pet = new Pet();
    pet.cry();
  }
}

// 멍멍~ 냐옹냐옹~
```

- Cat, Dog 인터페이스를 동시에 구현한 Pet 클래스에서만 cry() 메소드를 정의하므로, 앞의 예제에서 발생한 메소드 호출의 모호성이 없음

### 추상 클래스 vs 인터페이스

- 추상 클래스
  - 클래스
  - 추상 메소드 및 일반 메소드와 멤버도 포함 가능
  - 다중 상속 불가능
  - 상속을 받아 기능을 확장시키는데 목적
  - 공유의 목적
- 인터페이스
  - 클래스가 아님
  - 추상 메소드와 상수만을 멤버로 포함
  - 다중 상속, 구현 가능
  - 구현 객체의 같은 동작을 보장하기 위한 목적

<br>

# 직렬화

- Java 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 바이트 형태로 데이터를 변환하는 기술과, 바이트로 변환된 데이터를 다시 객체로 변환하는 기술(역직렬화)을 아울러서 이야기 함
- 시스템적으로 이야기하면, JVM의 메모리에 상주되어 있는 객체 데이터를 바이트 형태로 변환하는 기술과, 직렬화된 바이트 형태의 데이터를 객체로 변환해서 JVM으로 상주시키는 형태를 같이 이야기 함

<br>

# Generic

- 데이터의 타입을 일반화(generic)한다는 의미
- 클래스나 메소드에서 사용할 내부 데이터 타입을 **컴파일 시** 미리 지정하는 방법

#### 장점

- 클래스나 메소드 내부에서 사용되는 객체의 타입 안정성을 높일 수 있음
- Collection 내부에서 들어온 값이 내가 원하는 값인지 별도의 로직 처리를 구현할 필요가 없음

#### 선언 및 생성

```java
class MyArray<T> {
    T element;
    void setElement(T element) { this.element = element; }
    T getElement() { return element; }
}
```

- 'T' 를 타입 변수라고 하며, 임의의 참조형 타입을 의미
- T 뿐 아니라 어떠한 문자를 사용해도 상관 없으며, 여러 개의 타입 변수는 쉼표로 구분하여 명시
- ***클래스 뿐 아니라, 메소드의 매개변수나 반환값으로도 사용 가능***

```JAVA
MyArray<Integer> myArr = new MyArray<Integer>();
```

- 제네릭 클래스를 생성할 때, 사용할 실제 타입을 명시하면 내부적으로 정의된 타입 변수가 명시된 실제 타입으로 변환되어 처리

#### 제거 시기

- 제네릭 타입은 컴파일 시 컴파일러에 의해 자동으로 검사되어 타입 변환
- 이로 인해 모든 제네릭 타입은 제거되어 컴파일 class 파일에는 어떠한 제네릭 타입도 남아있지 않음
- 이런 식으로 동작하는 이유는 제네릭을 사용하지 않는 코드와의 호환성을 유지하기 위함
