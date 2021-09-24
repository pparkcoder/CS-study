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

