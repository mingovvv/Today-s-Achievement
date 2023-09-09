## @Qualifier, @Primary

----

스프링은 의존관계 주입을 위해 스프링 빈을 뒤지다가 동일한 타입의 빈이 2개 이상이라면 `NoUniqueBeanDefinitionException` 에러가 발생시킨다.
이를 해결하는 3가지 방법이 있다.

#### 1. @Autowired 필드명 매칭
`@Autowired`는 기본적으로 타입 매칭을 시도하고 2개 이상의 빈이 발견된다면 `필드 명`, `파라미터 명`으로 빈을 추가 매칭한다.

#### 2. @Qualifier 사용
빈 이름을 바꾸는 것이 아니라 추가 구분자의 개념이다. (@Qualifier 끼리 매칭)   
참고로 `@Qualifier`로 추가 구분자와 매칭되는 빈을 찾지 못하면 
bean name을 찾으니 알아두자.
아래 예제에서는 `fix`와 매칭되는 `@Qualifier`가 없었다면 `fix`라는 bean이 있는지 찾았을 것이다.
   
```java
@Component
@Qualifier("rate")      // bean name : rateDiscountPolicy
public class RateDiscountPolicy implements DiscountPolicy { }

@Component
@Qualifier("fix")       // bean name : fixDiscountPolicy
public class FixDiscountPolicy implements DiscountPolicy { }

@Component
public class MemberServiceImpl implements MemberService {

    private final DiscountPolicy discountPolicy;

    @Autowired
    public MemberServiceImpl(@Qualifier("fix") DiscountPolicy discountPolicy) {
        this.discountPolicy = discountPolicy;
    }
}
```

#### 3. @Primary 사용
`@Primary`가 우선권을 가진다.
   
```java
@Component
@Primary
public class RateDiscountPolicy implements DiscountPolicy { }

@Component
public class FixDiscountPolicy implements DiscountPolicy { }

@Component
public class MemberServiceImpl implements MemberService {

    // RateDiscountPolicy가 주입된다.
    private final DiscountPolicy discountPolicy;

    @Autowired
    public MemberServiceImpl(DiscountPolicy discountPolicy) {
        this.discountPolicy = discountPolicy;
    }
}
```