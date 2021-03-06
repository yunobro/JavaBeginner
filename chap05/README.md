# 참조타입

## 05-1 참조타입과 참조변수

### 기본타입(Primitive Type)

* 정수, 실수, 논리 타입

* 실제 값을 변수 안에 저장

### 참조타입(Reference Type)

* 객체의 번지를 참조하는 타입 ( 배열, 열거, 클래스, 인터페이스 )

* 메모리의 번지를 변수 안에 저장

* 번지를 통해 객체를 참조

* 변수의 값 = 힙 영역의 객체 주소



### JVM이 사용하는 메모리 영역

* **메소드 영역** : 
  * JVM이 시작할때 생성
  * 모든 스레드가 공유
  * ***(정적 필드, 상수, 메소드 코드, 생성자 코드)***
* **힙 영역** : 
  * ***객체, 배열***이 생성되는 영역
  * JVM 스택영역의 변수나 다른 객체 필드에서 참조
  * 참조하는 변수, 필드가 없다면 의미없는 객체가 됨 -> JVM이 이것을 쓰레기 취급하고 Garbage collector 실행시켜 자동 제거
* **JVM스택 영역** :
  * 메소드 호출 / 제거시마다 Frame push / pop
  * ***Frame 내부에 로컬 변수 스택*** 존재 : 기본타입, 참조 타입 변수가 push || pop
  * 스택영역에 변수 생성 시점 : 초기화시 (최초로 변수에 값이 저장될 때)
  * ***변수는 선언된 블록 안에서만 스택에 존재, 블록 벗어나면 스택에서 제거***

### 참조 변수 사용시 에러

```java
NullPointerException
```

참조 변수가 null 가지고 있는 경우, 참조 객체가 없으므로 변수를 통해 객체 사용 불가

null 상태에서 ~~사실없는~~ 객체의 데이터(필드)나 메소드 사용시 발생

### String

문자열 리터럴 동일시 String 객체 공유

### 객체 생성 연산자 (new)

힙 영역에 새 객체 만들 때 사용



## 05-2 배열

### 배열 

* 같은 타입의 데이터를 연속된 공간에 나열하고 각 데이터에 index를 부여해놓은 자료구조
* 객체이므로 힙영역에 생성

### 배열 생성

- 값 목록 이용 || new 연산자 이용

```java
// 값 목록 이용
String[] names1 ={"kim","seo","lee"};

// new 연산자 이용
String[] names2 = null;
names2 = new String[]{"kim","seo","lee"};

// 메소드 매개값 배열일 경우
int result = add ({95,80,20}) // compile error
int result = add (new int[]{95,80,20});

// 저장 배열 미리 만들고 싶은 경우
int[] scores = new int[30]; 
```

- 값 목록 이용시, 배열 변수 선언 후 다른 시랭문에서 중괄호 사용한 배열 생성 안 됨
- ***배열 변수 미리 선언 후 값이 나중에 결정되는 상황*** => new 연산자 사용
- ***매소드의 매개값이 배열일 경우*** => new 연산자 사용
- ***값 목록 모르지만 향후 저장 배열 미리 만들고 싶은 경우*** => new 연산자 사용
- New 이용시 배열 자동으로 기본값 ( 0 || false || null ) 으로 초기화됨 



### 배열 길이

```java
int[] ary = {10,20,30};
int num = ary.length; // 읽기 전용 필드기 때문에 값 쓰기 불가
```

### 배열의 인덱스 초과해서 사용시 에러

```java
ArrayIndexOutOfBoundException // 배열의 인덱스 0 ~ (length-1)
```

### 명령 라인 입력

```java
public static void main(Strin[] args){}
```

[ JDK 11 ~ ] java -p . -m 모듈명/패키지 arg0 arg1 arg2 arg3 ...

[~ JDK 8 ] java 패키지 arg0 arg1 arg2 arg3 ...

[Eclipse] Run - Run Configurations - Main - Project - Main class - Arguments

### 정수로 변환할 수 없는 문자열 주어질 경우 에러

```java
NumberFormatException
```

### 배열 복사

- 배열 생성시 크기 변경 불가능
- 더 많은 저장 공간 필요시 더 큰 배열 새로 만들고 복사
- for문 || System.arraycopy()

```java
System.arraycopy(arr1, 0, arr2, arr1.length);
```

### For문 심화

- 배열, 컬렉션 처리 쉽게

```java
int[] scores={1,2,3,4,5,6,7};
for(int score: scores){
  sum += score;
}
```



## 05-3 열거 타입

### 열거 타입

- 한정된 값만 갖는 타입 (봄,열,갈,결)

```java
public enum Week{
  SPRING,
  SUMMER,
  AUTUMN,
  WINTER
}
```

