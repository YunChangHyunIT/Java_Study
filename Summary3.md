# Summary3


## Collection
- 컬렉션이란 데이터의 집합, 그룹을 의미한다.
- JCF(Java Collections Framework)는 컬렉션과 이를 구현하는 클래스를 정의하는 인터페이스(공통된 메소드를 모아놓은)를 제공한다.
- Collection 인터페이스는 List, Set, Queue 크게 3가지 상위 인터페이스로 분류할 수 있다.
- Map의 경우 Collection 인터페이스를 상속받고 있진 않지만 Collection으로 분류된다.

![컬렉션](https://user-images.githubusercontent.com/58713853/73814627-f84d6400-4826-11ea-95dc-0de32bd8be6c.PNG)

- Collection 인터페이스의 특징

![컬렉션 특징](https://user-images.githubusercontent.com/58713853/73814690-229f2180-4827-11ea-8cf8-380b98c75a20.PNG)

### List 인터페이스
- 순서가 있는 데이터의 집합
- 색인을 사용하여 특정 위치에 요소를 삽입하거나 접근할 수 있으며 데이터의 중복을 허용한다.

- ArrayList
  - 상당히 빠르고 크기를 마음대로 조절할 수 있는 배열
  - 단방향 포인터 구조로 각 데이터에 대한 인덱스를 가지고 있어 조회 기능에 성능이 뛰어나다.
- Vector
  - 과거에 대용량 처리를 위해 사용한다.
  - 내부에서 자동으로 동기화처리가 일어나 비교적 성능이 좋지 않고 무거워 잘 쓰이지 않는다.
- LinkedList
  - 양방향 포인터 구조로 데이터의 삽입, 삭제가 빈번할 경우 데이터의 위치정보만 수정하면 되기에 유용하다. (빠른 성능을 보장)
  - 스택, 큐, 양방향 큐 등을 만들기 위한 용도로 쓰인다.
  
### Set 인터페이스
- 순서를 유지하지 않는 데이터의 집합
- 데이터의 중복을 허용하지 않는다.

- HashSet
  - 가장빠른 임의 접근 속도
  - 순서를 예측할 수 없다.
- TreeSet
  - 정렬된 순서대로 보관하며 정렬방법을 지정할 수 있다.
- LinkedHashSet
  - 추가된 순서 또는 가장 최근에 접근한 순서대로 접근 가능
  
### Map 인터페이스
- 키(Key), 값(Value)의 쌍으로 이루어진 데이터의 집합
- 순서는 유지되지 않으며 키(Key)의 중복을 허용하지 않으나 값(Value)의 중복은 허용한다.

- HashMap
  - Map 인터페이스를 구현하기 위해 해시테이블을 사용한 클래스 (아직 이게 무슨의미인지 파악하지 못함..)
  - 중복과 순서가 허용되지 않는다.
  - 키와 값으로 nll값이 올 수 있다.
- Hashtable
  - HashMap 보다는 느리지만 동기화 지원
  - 키와 값으로 null값이 허용되지 않는다.
- TreeMap
  - 이진검색트리의 형태로 키와 값의 쌍으로 이루어진 데이터를 저장
  - 정렬된 순서대로 키(Key)와 값(Value)을 저장하여 검색이 빠르다.
  - 저장시 정렬(오름차순)을 하기 때문에 저장시간이 다소 오래 걸린다.
- LinkedHashMap
  - 기본적으로 HashMap을 상속받아 HashMap과 매우 흡사
  - Map에 있는 엔트리들의 연결 리스트가 유지되므로 입력한 순서대로 반복 가능
  
  
참고 : https://gangnam-americano.tistory.com/41 \
https://hackersstudy.tistory.com/26

