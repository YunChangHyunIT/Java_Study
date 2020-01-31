# Summary2

## block 변수 / member field
- block 변수(메소드와 같이 블락안에 있는 변수)와 member field의 이름이 같으면 block 변수가 우선순위가 높다.

## Wrapper Class
- 참조타입을 기본타입으로 바꿀때 사용하는 클래스
- 기본타입의 앞글자를 대문자로 만들면 클래스명이 된다.
- ex) Boolean, Byte, Integer, Float, Character...

## boxing / unboxing
- boxing : 기본타입을 참조타입으로 바꾸는 것
- unboxing : 참조타입을 기본타입으로 바꾸는 것
```java
// 기 : 기본타입 / 참 : 참조타입
int a = 10;
Integer aa = new Integer(a) // 기 -> 참
Integer aa2 = 10; // 기 -> 참
int c = aa2; 참 -> 기
int c1 = aa.intValue(); // 참 -> 기

Object o = 10; // 기 -> 참
int d = (Integer)o; // 참 -> 기
```

## java.lang.Object의 4대 메소드
- equals, toString, hashcode, getClass

### equals
- boolean equals(Object o)
- 객체끼리 같은지를 판단할 때 사용하는 메소드
- equals를 오바라이딩해서 값이 같으면 객체가 같다라고 판단하게 만들 수 있다.
  
```java
A a = new A();
A a2 = new A();
System.out.println(a.equalse(a2)); // false

String str = new String("자바");
String str2 = "자바";
str.equals(str2); // true (오버라이딩 했다고 가정)
```

### toString
- String toString()
- 문자열 타입으로 변경시켜주는 메소드
- toString을 오버라이딩하면 객체를 print할 시, toString이 호출 된다.

### hashcode
- int hashcode()

### getClass
- Class getClass()
- 객체의 package명 + 클래스이름을 가져오는 클래스 타입의 메소드
