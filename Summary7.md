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

// Tv클래스가 있다고 가정
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

public static void main(String[] args) {
  Box<Integer> box = <Integer>boxing(100);  // 구체적으로 타입지정
  Box<Integer> box = boxing(100); // 타입 파라미터를 Integer로 추정
}
```

## 제한된 타입 파라미터
- 상속 및 구현관계를 이용해서 타입을 제한 할 수 있다.
- 타입 파라미터를 대체할 구체적인 타입
  - 상위타입이거나 하위 또는 구현 클래스만 지정할 수 있다.
- 메소드의 중괄호{}안에서 타입 파라미터 변수로 사용 가능한 것은 상위 타입의 멤버(필드,메소드)로 제한된다.
- 하위 타입에만 있는 필드와 메소드는 사용할 수 없다.

### 선언방법
- public <T extends 상위타입> 리턴타입 메소드명(파라미터 변수, ...) {}
  - 상위타입은 클래스 뿐만 아니라 인터페이스도 가능하다.
  - 인터페이스라고 해서 implements를 사용하지 않고 extends로 사용한다.

#### 예제 코드
```java
public class Util {
  public <T extends Number> int compare(T t1, T t2) {
    double v1 = t1.doubleValue(); // Number클래스에 있는 doubleValue() 메소드 사용가능
    double v2 = t2.doubleValue();
    return Double.compare(v1,v2);
  }
}

public static void main(String[] args) {
  int result = Util.compare(10,20); // 문자열을 넣을 시 오류가 발생한다.
  System.out.println(result);
}
```
## 와일드 카드(?)의 타입
- 제네릭 타입을 파라미터변수나 리턴타입으로 사용할 때 타입 파라미터를 제한할 목적으로 사용

### 와일드 카드의 세가지 타입

![상속이미지](https://user-images.githubusercontent.com/58713853/74127153-1b0fbc00-4c1d-11ea-8e73-88171a6ad427.jpg)
<br> 이미지 출처 : https://zbomoon.tistory.com/13

- 제네릭 타입<?> : Unbounded Wildcards(제한없음)
  - 타입 파라미터를 대치하는 구체적인 타입으로 모든 클래스나 인터페이스 타입이 올 수 있다.
- 제네릭 타입<? extends 상위타입> : Upper Bounded Wildcards (상위 클래스 제한)
  - 타입 파라미터를 대치하는 구체적인 타입으로 명시한 상위타입이나 그 상위타입을 상속받는 하위타입만 올 수 있다.
  - 제한된 타입 파라미터랑 비슷한 기능을 한다.
  - ex) <? extends 공룡> 을 하게되면 공룡, 투슬리스, 둘리 가 올 수 있다.
- 제네릭 타입<? super 하위타입> : Lower bounded Wildcards (하위 클래스 제한)
  - 타입 파라미터를 대치하는 구체적인 타입으로 명시한 하위타입이나 그 하위타입이 상속받은 상위타입이 올 수 있다.
  - ex) <? extends 멍멍이>을 하게되면 포유류, 동물이 올 수 있다.
  
## Stream(스트림)
- 스트림은 컬렉션(배열포함)의 요소를 하나씩 참조해서 람다식을 처리할 수 있는 반복자이다.
- 람다식으로 요소 처리 코드를 제공한다.
  - 스트림이 제공하는 대부분의 요소처리 메소드는 함수형 인터페이스의 파라미터 타입을 가진다.
  - 파라미터 값으로 람다식 또는 메소드 참조를 대입할 수 있다.
- 내부 반복자를 사용하게 되어 병렬 처리가 쉬워진다.
  - 외부 반복자 : 개발자가 코드로 직접 컬렉션 요소를 반복해서 요청하고 가져오는 코드 패턴
  - 내부 반복자 : 컬렉션 내부에서 요소들을 반복시키고 개발자는 요소당 처리해야할 코드만 제공하는 패턴
- 내부 반복자의 이점
  - 개발자는 요소 처리 코드에만 집중하게 한다.
  - 멀티 코어 CPU를 최대한 활용하기 위해 요소들을 분배시켜 병렬처리 작업을 할 수 있다.
  
### 병렬(parallel)처리
  - 한가지 작업을 서브작업으로 나누고 서브작업들을 분리된 스레드에서 병렬적으로 처리한 후 서브 작업들의 결과들을 최종 결합하는 방법
  - 자바는 ForkJoinPool이라는 프레임워크를 이용해서 병렬 처리를 한다. (JAVA API)

```java
public class Print {	// 메소드 참조를 사용하기 위한 객체
	public void print(String a) {
		System.out.println(a+",");
	}
}

public class StreamTestMain {
	public static void main(String[] args) {
    List<String> list = Arrays.asList("수지","설현","BTS");
        
		// 순차적 처리 
		Stream<String> stream = list.stream();
		stream.forEach(s -> { 
			System.out.println(s);  // 람다식을 사용하여 요소처리
		});
		
		// 병렬로 처리 
		Stream<String> parallelStream = list.parallelStream();
		parallelStream.forEach(s -> {
			System.out.println(s);
		});
    
    // 배열로 부터 스트림 얻기 
		ParallelExam p = new Print(); // 메소드 참조를 위한 객체 생성
		String[] strArray = {"홍길동1","홍길동2","홍길동3","홍길동4","홍길동5"};
		Stream<String> strStream = Arrays.stream(strArray);
		strStream.forEach(p::print);  // 메소드 참조
		
		// 숫자 범위로 부터 스트림 얻기
		// IntStream stream = IntStream.range(1, 100); // 1-99
		IntStream stream = IntStream.rangeClosed(1, 100); // 1-100
		stream.forEach(a ->{
			int sum=0;
			sum += a; 
			System.out.println("합 : "+sum);
		});
    
  }
}

```

## 스트림 파이프라인
- 파이프라인 : 여러 개의 스트림이 파이프처럼 연결되어 있는 구조
- 스트림은 중간처리와 최종처리를 파이프라인(pipelines)으로 해결한다.

### Reduction (리덕션)
- 대량의 데이터를 가공해서 축소하는 것을 말한다.
  - 합계, 평균, 카운팅, 최대값, 최소값등을 집계하는 것
- 요소가 리덕션의 결과물로 바로 집계할 수 없을 경우 중간처리가 필요하다.
- 중간처리한 요소를 최종처리해서 리덕션 결과물을 산출한다.

### 중간처리
- 중간처리 메소드는 필터링, 매핑, 정렬, 그룹핑등이 있다.
- 중간처리 메소드는 리턴타입이 스트림이다.

### 최종처리
- 최종처리 메소드는 합계, 평균, 카운팅, 최대값, 최소값등이 있다.
- 최종처리 메소드는 리턴타입이 기본타입이거나 OptionalXXX 이다.

### 파이프라인 형성 과정
1. 중간처리 메소드는 중간처리 된 스트림을 리턴한다.
1. 이 스트림에서 다시 중간처리 메소드를 호출해서 파이프 라인을 형성하게 된다.
1. 스트림소스(컬렉션, 배열, 파일) -> 오리지널(중간) -> 필터로 처리(중간) -> 매핑처리(중간) -> 집계처리(최종)
- 최종 스트림의 집계기능이 시작되기 전까지 중간처리는 지연(lazy)된다.
  - 최종 스트림이 시작하면 비로소 컬렉션에서 요소가 하나씩 중간스트림에서 처리되고 최종스트림까지 오게 된다.

#### 예제코드
- distict()
  - Stream에서는 equals() 메소드가 true로 나오면 동일한 객체로 판단하고 중복을 제거
  - IntStream, LongStream, DoubleStream에서는 동일 값일 경우 중복을 제거
- filter()
  - 파라미터 값으로 주어진 Predicate가 true를 리턴하는 요소만 필터링
  - Predicate : 수학에서 결과로 true 또는 false를 반환하는 함수
- mapToInt()
  - 주어진 함수를 스트림의 요소에 적용한 결과를 IntStream으로 반환한다.
- getAsDouble()
  - 이 안에 값이 있으면 값을 OptionalDouble을 반환하고 그렇지 않으면 throw NoSuchElementException을 반환한다.
  - OptionalDouble : double 값을 가지고 있는지 아닌지를 나타내는 컨테이너 클래스 (해당 객체 안에 값이 존재하면 그 값을 반환하고 없으면 other를 반환합니다.
  
```java
public class Member {
	public static int MALE = 0; 
	public static int FEMALE = 1;
	
	private String name; 
	private int sex; 
	private int age; 
	
	public Member(String name, int sex, int age) {
		this.name = name;
		this.sex = sex;
		this.age = age;
	}

	public int getSex() {
		return sex;
	}

	public int getAge() {
		return age;
	}
}

public static void main(String[] args) {
		List<String> names = Arrays.asList("정인선","조수아","정인선","배수지","조두산","조형기");
    
   		names.stream()
			.distinct()
			.filter(n -> n.startsWith("배"))
			.forEach(n -> System.out.println(n));
        
		List<Member> list = Arrays.asList(
			new Member("홍길동1", Member.MALE, 10),
			new Member("홍길동2", Member.MALE, 20),
			new Member("홍길동3", Member.MALE, 30),
			new Member("홍길동4", Member.MALE, 10)
		);
    
		double ageAvg = list.stream()            // 오리지널 스트림
			.filter(m -> m.getSex()==Member.MALE)// 
			.mapToInt(Member::getAge)            // 중간
			.average()                           // 최종
			.getAsDouble();
		
		System.out.println("남자들의 평균 나이 : "+ageAvg);   
	}

```
