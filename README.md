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

### Item 15. 

### Item 16. 

### Item 17.

### Item 18. 

### Item 19. 

