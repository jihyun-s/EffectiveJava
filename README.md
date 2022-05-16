# Effective Java 

## Chapter 2. 객체의 생성과 파괴

### Item 1. Constructor 대신 Static Factory Method를 고려하라
    (+) 장점 
        1. 이름을 가질 수 있다. 
        2. Simple하고 명확하게 사용할 수 있다. 
        3. 인스턴스를 매번 생성할 필요는 없다. 
            Flyweight pattern - Collection Object 
            Singleton pattern - Single Object 
            (Singleton의 경우 한 객체, Flyweight의 경우 multiple한 객체를 다룬다.) 
    
    (-) 단점
        1. Static Factory method만 제공하면 Constructor가 없을 수 있어 상속받은 Class를 만들 수 없다. 
        2. 프로그래머에게 인지가 잘 되지 않을 수 있다.
    
### Item 2. 많은 parameter가 있는 Constructor는 Builder를 고려하라
    (+) 장점
        - 상속받은 Class의 Builder가 정의한 build 메서드가 
        상위 메서드의 타입을 return하는 것이 아닌 자신의 타입을 return한다. 
        
    (-) 단점 
        1. Builder를 항상 만들어야 하기 때문에 생성 비용이 무조건 생긴다. 
        2. 점층적 생성자 패턴(Argument를 여러개 가진 Constructor)보다 장황하여 
        적은 갯수의 Parameter일 경우 오히려 좋지 않을 수 있다. 
        
### Item 3. private constructor나 enum Type으로 Singleton임을 보증하라 

### Item 4. Instance화를 막으려면 private constructor를 사용하라 

### Item 5. Resource를 직접 명시하지 말고, Dependancy Injection을 사용하라 
    - 생각해봐야 할 것
        - Config Class를 생각없이 사용하고 있지는 않았는지
        - Singleton을 이해하고 있는지 
        - Dependency Injection(DI)를 잘 이해하고 있는지 
        
### Item 6. 불필요한 객체 생성 금지 
    - Boxing type 대신 Primitive Type을 권장 (ex. Long 대신 long) 
    - 그렇다고 항상 primitive type이 옳은 것은 아니다. (ex. 물건의 가격이 0인 것과 null인 것의 의미는 다르다.) 
    
    - 생각해봐야 할 것
        - 무심결에 Instance를 과도하게 생성하지는 않았는지
        - Primitive Type과 Boxing Type을 의도하고 사용하였는지 
       
### Item 7. 다 쓴 객체 참조를 해제하라 
    - 우아하게 참조를 해제하는 법 
        - 유효 Scope 밖으로 넘어가면 자동으로 GC의 대상이 된다. (Unreachable Object가 되었을 때) 

    - 생각해봐야 할 것 
        - Array를 잘 쓰고 있었는지? 
        - 메모리 구조에 대해 이해하고 있는지 : Heap, Stack, Method Area 등 
        - Gabage Collector가 동작하는 원리에 대해 잘 이해하고 있는지 
        - JVM 
        
### Item 8. finalizer, cleaner를 피하라 
    - 특수한 상황이 아니라면 사용하지 않는 것을 추천
    - 안전망 역할로 아주 제한적으로 사용 가능함 
    
### Item 9. try-finally 대신 try-with-resources 


## Chapter 3. 모든 객체의 공통 메서드

### Item 10. equals의 일반 규약을 지켜 재정의하라. 
    - Equals의 전형적인 검사 패턴
        1. ==를 통해 input이 자기 자신의 참조인지 
        2. Instanceof(or getClass)를 통해 input의 타입이 명확한지 
        3. 2를 통해 검사한 객체를 올바른 타입으로 형변환 
        4. 핵심 필드들이 모두 일치하는지 
        5. [not null] if x is not null, then x.equals(null) => false 
    
    - Override시 주의사항 
        1. 만족해야 하는 조건을 만족시켰는가 
        2. Equals를 재정의할 때 hascode도 재정의하였는가 
        3. Equals의 input이 Object인가 (Overriding 하였는가) 
        4. 핵심 필드들이 모두 일치하는지 
        5. [not null] if x is not null, then x.equals(null) => false 
        
### Item 11. equals를 재정의하려거든 hascode도 함께 재정의하라     
    - == : primitive type일 때는 value compare, reference type일 때는 주소가 같은지 비교 
    - equals() : 같은 객체인지 (default는 ==과 동일함, oveerride하여 사용) 
    - hashcode() : 논리적으로 같은 객체라면 같은 hashcode를 반환해야 한다. 
    
    - equals는 필요할 때 적재적소에 활용하자 
    - equals를 override한다면 hashcode의 override는 필수 
    - Lombok을 사용한다면 @Data, @EqualsAndHashcode의 동작원리 확인

### Item 12. toString을 항상 override하라 
    - toString의 default value : className@16진수 hashcode
    - Lombok의 @ToString 
    
    - 로그를 찍을 일이 있으면 toString을 overriding
    - 전부 다 toString으로 출력하지 말고, 필요한 것 위주로 작성 

### Item 13. clone 재정의는 주의해서 사용하라 
    - Clone은 
        Primitive type의 배열이 아니면 쓰지 말자 
        Copy Constructor or Copy Factory method를 활용하라 
        Cloneable을 확장하지마라 

### Item 14. Comparable을 구현할지 고려하라 
    - compareTo의 규약 (equals와 비슷) 
        - 객체와 주어진 객체의 순서를 비교한다. 
        - 이 객체가 주어진 객체보다 작으면 음의 정수, 같으면 0, 크면 양의 정수를 반환. (-1, 0, 1)
        - 비교할 수 없을 땐 ClassCastException
        
    - 필요하다면 적절하게 Comparable을 구현하여 compareTo으 ㅣ이점을 누릴 수 있다. 
    - 하지만 정렬의 기준이 고정이 아니라면, 다른 방식(ex. Method, service를 통한 조건 별 ordering)을 고려해 볼 수 있다. 


## Chapter 4. 클래스와 인터페이스 

### Item 15. 클래스와 멤버의 접근 권한을 최소화하라
    - public class의 instance field 
        1. public으로 열 경우 thread safe하지 못하다. (Lock류의 작업을 걸 수 없음) 
        2. 꼭 필요한 상수라면 예외적으로 public static final로 공개할 수 있다. 
        3. [주의사항] public static final Thing[] VALUES = {...} 는 수정이 가능하다. 

    - 위 3번 배열의 두 가지 해결책 
        - 배열을 private으로 만들고, 불변 리스트를 추가 
            1. 읽기전용으로 response
            2. 원본이 바뀔 경우 같이 변경됨 
        - 배열을 private으로 두고, 복사본을 반환하는 public method 
            1. 해당 시점으로 clone됨. 
            2. 원본이 바뀔 경우 같이 변경되지 않음 
     
### Item 16. public class에서는 get method를 통해 필드에 접근하라
    - 생각해볼만한 점 
        - 캡슐화는 꼭 한 번 다시 점검해보자.
        - 접근제어자는 습관적으로 항상 최소로 사용하자.

### Item 17. 변경 가능성을 최소화하라 
    - Immutable class 불변 클래스 (내부를 수정할 수 없음)
        1. 상태 변경 method(ex. Set method)를 제공하지 않는다. 
        2. Class 확장힞 않도록 한다. (ex. Final) 
        3. 모든 field를 final로 선언한다. 
        4. 모든 field를 private으로 선언한다. 
        5. 자신을 제외하고는 아무도 가변 컴포넌트에 접근할 수 없도록 한다. 
        
    - BigInteger (Immutable class example) 
        - Immutable class의 조건
            1. Thread safe 
            2. failure atomicity - 예외가 발생 후에도 유효한 상태 
            3. 값이 다르면 무조건 독립적인 객체로 생성되어야 함 
        - 중간 단계 (객체가 완성 중인 상태)를 극복하기 위한 방법
            - statif factory method를 통해 new instance를 생성해 response (ex. StringBuilder) 
     
    - 습관적으로 Setter를 만들지 말자 (setter가 불필요할 수도 있다.)
    - Class는 꼭 필요한 경우가 아니면 불변이어야 한다. (특히 단순한 Value Object는 더 그러함)
    - 모든 클래스가 불변일 수 없지만, 변경할 수 있는 부분을 최대한 줄여보자. 
            
### Item 18. 상속보다는 컴포지션을 사용하라
    - Composite pattern ( composite : 합성 ) 
    - 상속은 캡슐화를 해칠 수 있기 때문에 pure한 is-a 관계일 때만 써야 한다. 
    - Wrapper class(Drawer)가 class를 확장하여 사용하는 것보다 더 견고하다. 

### Item 19. 상속을 고려해 설계하고 문서화하라. 그러지 않았다면 상속을 금지하라 
    - 상속을 금지하는 방법
        - Class를 final로 선언 
        - 모든 생성자를 private or package-private로 선언하고 public static facotry로 만들기 
     
    - 올바르게 상속을 고려하려면 
        - @implSpec을 통해 상속할 때 필요한 내용을 서술한다. 
        - Clone과 readObject 모두 직/간접적으로 재정의 가능 method를 호출해서는 안 된다. 
        - 검증방법 : 하위 Objecct를 만들어 테스트 해보면 좋다. 
         
    - 상속보다는 interface를 통한 구현을 추천
    - 변수 몇 개가 겹친다고해서 꼭 상속을 통한 확장을 해야한다는 것을 의미하는 것은 아니다. 
    
### Item 20. Abstract class보다는 interface를 우선하라 
    - class의 extends는 하나만 가능 
    - interface의 implements는 여러개 가능 
    - Skeletal implementation (추상 골격 구현) 
        1. Interface로 뼈대를 만들고
        2. Abstract class로 필요한 구현을 모두 마친 후 
        3. Subclass로 마무리하는 것
        * 주의사항 : Object method(equals, toString, ...)는 default 메서드로 제공하면 안된다. 
    - 뼈대를 만들 때에는 default method가 대안이 될 수 있다. 
    
### Item 21. 인터페이스는 구현하는 쪽을 생각해 설계하라 

### Item 22. 인터페이스는 타입을 정의하는 용도로만 사용하라 
    - Constant static final은 anti pattern 
        - 클래스 내부에서 사용하는 상수는 내부 구현에 해당된다. 
        - 차라리 클래스에 static final로 추가하는 것이 더 낫다. 
        - 여러 곳에서 사용해야 할 값이라면 util class 
    - 인터페이스를 타입으로 정리하는 용도로만 쓰고 상수 공개용으로 사용하지 마라. 필요하다면 Class에 담아라 
    - Properties에 값을 선언해 두고 injection을 하는 것도 방법일 수 있다.

### Item 23. 태그 달린 클래스보다는 클래스 계층구조를 활용하라
    - 태그 달린 클래스를 써야 하는 상황은 거의 없다. 
    - 이미 태그가 달려 있다면, 계층 구조로 리팩토링 하는 것을 생각해보자

### Item 24. 멤버 클래스는 되도록 static으로 만들라 
    - Nested class 
        - Method 밖에서 사용할 것이다 - member class
            - 그 중 member class가 바깥 instance를 참고한다 -> non-static 
            - 그 외 -> static 
        - 딱 한 곳에서 사용하고 사전 struct가 있다 -> Anonymous class 
        - 그 외 -> local class

### Item 25. Top level 클래스는 한 파일에 하나만 담아라


## Chapter 5. 제너릭

### Item 26. 로 타입은(raw type) 사용하지 말라 
    - (예외) Class 리터럴에는 raw type을 써야 한다. 
    - 예외적인 케이스를 제외하면 명확히 타입을 명시하도록 하자. 

### Item 27. 비검사 경고를 제거하라 
    - Compiler가 보내는 warning을 제거하라 
    - 만약 안전하다고 확신할 수 있으면 @SuppressWarnings("unchecker")를 통해 경고를 숨기자.
    
### Item 28. 배열 대신 리스트를 사용하라 
    - 코딩 테스트 환경에서는 Array가 미세하게 더 유리할 수는 있겠지만, Product level에서는 ArrayList만으로도 충분하다.

### Item 29. 이왕이면 제네릭 타입으로 만들라 
    - E : Element 
    - K : Key 
    - N : Number 
    - T : Type
    - V : Value 
    - Object를 이용한 직접 형변환하는 코드 대신 제네릭 타입으로 만들어 형변환하는 코드를 없애라. 

### Item 30. 이왕이면 제네릭 메서드로 만들어라
    - 제네릭 타입과 같이 형변환 해야하는 메서드보다 제네릭 메서드가 더 안전하고 사용하기도 쉽다 
    - 형변환 해야 하는 메서드는 제네릭하게 만들자

### Item 31. 한정적 와일드카드를 사용해 API 유연성을 높여라 
    - List<? extends Number> (super도 가능) 

### Item 32. 제네릭과 가변 인수를 함께 쓸 때는 신중하라 
    - Variadic Arguments (가변 인수) 
        - 메서드의 argument의 개수를 클라이언트가 조절할 수 있게 한다. 
        - 또한 반드시 한 개의 가변 인수만을 사용해야 하며 맨 마지막 Argument로 사용해야 한다. 
    
    - @SuppressWarnings (컴파일 경고 숨기기) 
    - @SafeVarargs (메서드의 타입 안정성을 보장함) 

    - 제네릭 배열에 아무것도 저장하거나 덮어쓰지 말고 배열의 참조를 밖으로 노출시키지 말아야 한다. 
    
### Item 33. 타입 안정 이종 컨테이너를 고려하라 


## Chapter 6. 열거 타입과 어노테이션 

### Item 34. int 상수 대신 enum을 사용하라 
    - fromString method (자주 쓰이는 pattern) 
        - 타 서버에서 불확실성을 가지고 enum이 넘어오거나 db 등의 값을 처리할 때 유용할 수 있다. 
        - ex. String으로 받아와서 enum으로 변환 
    - Enum화 시킬 수 있는 상황이면 가급적 하는 것이 좋다.
    - 외부 type의 symbol이 불안정하다면 fromString을 통한 방안도 고려할만하다.
        
### Item 35. ordinal method 대신 instant field를 사용하라 
    - Enum에서 ordinal()로 enum의 번호를 반환해줌 
    - Ordinal는 EnumSet, EnumMap과 같이 열거 타입 기반의 자료구조에 사용
    
### Item 36. bit field 대신 EnumSet을 사용하라 

### Item 37. ordinal indexing 대신 EnumMap을 사용하라 

### Item 38. 확장할 수 있는 열거 타입이 필요하면 인터페이스를 사용하라 

### Item 39. 명명 패턴보다 Annotation을 사용하라 

### Item 40. @Override 어노테이션을 일관되게 사용하라 
    - @Override annotation을 사용하지 않아도 되는 경우
        - 추상 메서드를 재정의할 때

### Item 41. 정의하려는 것이 타입이라면 마커 인터페이스를 사용하라 

##

