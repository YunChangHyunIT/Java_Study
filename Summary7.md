# Summary7

## 멀티타입 파라미터
- 두개 이상의 타입 파라미터를 사용해서 제네릭타입을 선언할 수도 있다.

```java
class A<K,V,...> {}
interface IB<K,V,...> {}

public class Product<T,M> {
  private T kind;
  private M model;
  
  public T getKind() { return this.kind; }
  public M getModel() { return this.model; }
  
  public void setKind(T kind) { this.kind = kind; }
  public void setModel(M model) { this.model = model; }
}

Product<Tv,String> product = new Product<Tv,String>();
Product<Tv,String> product = new Product<>();
```

## 제네릭 메소드
- 파라미터 변수 타입과 리턴 타입으로 타입 파라미터를 갖는 메소드를 말한다.

### 제네릭 메소드 선언방법
- 리턴 타입 앞에 "<>" 기호를 추가하고 타입 파라미터를 기술한다.
- 타입 파라미터를 리턴타입과 파라미터 변수에 사용한다.

### 제네릭 메소드를 호출하는 두가지 방법
- 명시적으로 구체적인 타입을 지정하는 방법
  - 리턴타입 변수 = <구체적 타입> 메소드명(파라미터 값)
- 파라미터값을 보고 구체적 타입을 추정하는 방법
  - 리턴타입 변수 = 메소드명(파라미터 값);
  
#### 예제 코드
```java
public class Box<T>{
  private T t; 

  public void set(T t){
     this.t = t;
  }
  public T get(){
     return t;
  }
}

public class Util {
  public static <T> Box<T> boxing<T t) {  
  // public static <타입 파라미터,...> 리턴타입 메소드명(파라미터 변수,...) {}
  // Box<T>와 boxing(T t)에 들어갈 T를 명시해주는 것
    Box<T> box = new Box<T>();
    box.set(t);
    return box; // 리턴타입이 Box<T>기 때문에 box를 리턴
  }
}

Box<Integer> box = <Integer>boxing(100);  // 구체적으로 타입지정
Box<Integer> box = boxing(100); // 타입 파라미터를 Integer로 추정
```

## 제한된 타입 파라미터
- 상속 및 구현관계를 이용해서 타입을 제한 할 수 있다.
