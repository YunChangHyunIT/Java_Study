# Summary4

## interface(인터페이스)
- 추상 메소드로만 이루어진 클래스
- 인터페이스의 추상 메소드를 구현하지 못하면 자식 클래스는 추상 클래스가 된다.
- 기본 접근제한자는 보통 public을 사용한다.
- 변수는 자동으로 상수가 된다.
  - int A 를 선언할 때 원래의 멤버필드라면 0으로 디폴트 값이 들어가지만 interface는 선언할 수 없다.
  - int A = 10; 처럼 상수값을 넣어주어야한다.
- 인터페이스는 여러개의 인터페이스를 상속할 수 있다.
  - 인터페이스끼리 상속할때는 extends 키워드를 사용한다.
- 인터페이스를 상속하는 키워드는 implements이다.
- 일반 클래스와 인터페이스가 있을 경우에는 일반 클래스가 우선이다.


```java
// 인터페이스 선언 / 상속
public interface IA { // 인터페이스 선언
  void print();
}

public interface IB extends IA { // 인터페이스 선언, 인터페이스끼리 상속

}

public class A {  // 클래스 선언

}

public class B {  // 

}

```
