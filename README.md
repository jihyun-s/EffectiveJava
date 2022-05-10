# Effective Java 

## Chapter2. 객체의 생성과 파괴

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

###
