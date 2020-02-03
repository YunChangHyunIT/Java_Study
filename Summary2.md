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
- 객체끼리 값이 같은지를 판단할 때 사용하는 메소드
- 모든 객체가 상속받는 Object클래스에 정의되어 있지만 단순히 == 연산자로 참조값이 같은지를 비교한다.
	- 그렇기 때문에 동일한 값을 같더라도 true가 나오지 않고 false가 나온다.
- Object클래스의 equals를 오바라이딩해서 값이 같으면 객체가 같다라고 판단하게 만들 수 있다.
	- String 클래스가 대표적인 예이다.
  
```java
// String class
 public boolean equals(Object anObject) {
        if (this == anObject) {		// 기본적인 참조값 비교
            return true;
        }
        if (anObject instanceof String) {	// String 값을 하나하나 받아서 비교
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
```

### toString
- String toString()
- 문자열 타입으로 변경시켜주는 메소드
- toString을 오버라이딩하면 객체를 print할 시, toString이 호출 된다.

```java
A a = new A(); // 
System.out.println(a); // 객체의 메모리 주소가 나x온다

// A 클래스 안에 toString을 오버라이딩 한 후
@Override
	public String toString() {
		return "People [name=" + name + ", age=" + age + "]";
	}
  
System.out.println(a2); // People [name= "내가 넣은이름", age= "내가 넣은 나이"] 가나온다.
```

### hashcode
- int hashCode()
- 객체를 식별할 하나의 정수값을 말한다.
- equals()가 true인 두 Object를 HashMap에 put을 할 때 동일한 key로 인식하고 싶은 경우에 사용한다.
- HashSet, HashMap, HashTable 등등.. 에서 HashCode()의 리턴값이 true 이고 equals()의 리턴값이 true이면 동일한 객체로 본다.
	- 다만 hash 코드값이 같다고 해서 객체의 참조 값이 같은 것은 아니다.
```java
// int형 num 멤버 필드를 가지고 있고 equals()가 오버라이딩된 A라는 클래스가 있고 가정한다.

A c1 = new A(10);
A c2 = new A(10);
// 멤버 필드가 같은 객체를 생성한다.

System.out.println(c1.equals(c2)) // true

Map<A, Integer> map = new HashMap<A, Integer>();
map.put(c1, 1);
map.put(c2, 1);
System.out.println(map.size()); // hashCode를 오버라이딩 했으면 같은 객체로 판단하므로 1, 아니면 2가 나온다.


// hashCode 오버라이딩 부분 (num 값이 같으면 hashCode가 같아진다.)
// hashCode 연산 할 때는 소수를 사용한다. (이점은 분명하지 않지만.. 그렇게 사용되어왔다.)
public int hashCode() {
	final int prime = 31;
	int hashCode = 1;

	hashCode = prime * hashCode + num;

	return hashCode;
}
```


### getClass
- Class getClass()
- 객체의 package명 + 클래스이름을 가져오는 클래스 타입의 메소드
- toString으로 객체를 표현할 때 사용할 수 있다.
		
```java
// 위에 A클래스의 toString을 오버라이딩 한다고 가정한다. (A클래스는 edu라는 패키지에 속해있다고 가정한다.)
public String toString() {
        Class c = getClass();
        return "<" + c.getName() + ": num =" + num  + ">"; 
    }

// main 부분
A a = new A(12);
System.out.println(a); // <edu.A : num = 12> 라는 결과가 나온다.
// getName()을 사용하지 않고 getSimpleName() 을 사용할 시 edu.A가 아닌 A라고만 나온다.
```

- 클래스에서 속성을 뽑아 낼 때 사용할 수 있다.
	- 일반적인 프로그래밍에서 수행하진 않지만 프레임워크에서 자주 수행된다고 한다. (정확하진 않음)
	
```java
A a = new A(12);

Class c = a.getClass();

for (Field f : c.getDeclaredFields()) {	// getDeclaredFields : 해당 클래스에서 정의된 변수 목록을 field 클래스 배열 타입으로 리턴한다.
	f.setAccessible(true); // setAccessible : private 접근제어 선언이 되어 있는 경우, 접근을 가능하게 해준다.
	try {
	     System.out.println(f.getName() + " = " + f.get(a));
	} catch (Exception e) {
	     e.printStackTrace();
	}
}

// num = 12 라는 결과가 나온다. (물론, 필드가 더 있다면 다른 필드도 나올 것이다.)
// 이런식으로 필드를 뽑아내면 캡슐화의 의미가 있을까? 라는 의문이 들었지만 try catch로 예외처리를 해주면 된다.
```
