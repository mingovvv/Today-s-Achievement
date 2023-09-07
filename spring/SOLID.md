# SOLID
### 로버트 마틴이 제안한 좋은 객체 지향 설계의 5원칙

-----

1. SRP : 단일 책임 원칙(single responsibility principle)
   > 하나의 클래스는 하나의 **책임**을 가져야 한다. <br>
여기서 의미하는 **책임**은 변경이 발생 하였을 때, 그에 따른 파급효과가 작은 것이 **단일 책임 원칙**을 잘 따랐다고 볼 수 있다. <br><br>
ex) DTO를 내부에 객체 생성을 위한 정적메서드를 만들어 객체의 생성과 사용을 분리

2. OCP : 개방-폐쇄 원칙(open/closed principle)
   > 확장에는 열려있으나 변경에는 닫혀 있어야 한다. <br>

3. LSP : 리스코프 치환 원칙(liskov substitution principle)
   > 객체는 프로그램 대원칙의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다. <br>
   다형성에서 하위 클래스는 인터페이스 규약을 지켜야한다는 의미와도 같다. <br><br>
ex) 자동차 인터페이스에서는 엑셀은 *전진한다*는 대원칙을 기반으로 설계되었다. 하지만 이를 구현하는 객체에서 엑셀에 *후진한다*의 기능을 넣어도 컴파일 단계에서는 에러가 발생하지 않지만 LSP원칙을 위반하였기 때문에 좋은 객체 지향 설계가 아니다.
   
4. ISP : 인터페이스 분리 원칙(interface segregation principle)
   > 특정 클라이언트를 위한 인터페이스는 범용 인터페이스보다 여러개의 분리된 인터페이스를 사용하는 것이 좋다. <br>
   인터페이스가 명확해지고, 대체 가능성이 높아진다. <br><br>
ex) *자동차 인터페이스* -> *운전 인터페이스*, *정비 인터페이스* 로 분리

5. DIP : 의존관계 역전 원칙(dependency inversion principle)
   > 구체화에 의존하지 말고 추상화에 의존해야 한다. <br>
   클라이언트 코드에서 구현 클래스를 의존하지 말고 인터페이스를 의존하라는 의미. 즉, 역할과 구현을 철저하게 분리 <br><br>
ex) 배우의 경우, 배역이라는 역할(interface)에 의존해야지 배역을 맡은 배우(implement class)에게 의존하면 안된다.


----
#### 예제코드
``` java
class MemberService {
   
   // 메모리 DB - 사용안함 주석처리
   // MemberRepository m = new MemoryMemberRepository();
   
   // Jdbc DB - 사용
   MemberRepository m = new JdbcMemberRepository();
   
   ...
   
}
```
#### OCP, DIP 위반발생
> 위 코드는 MemberService 에서 구현클래스를 직접 선택하고 있어 OCP, DIP 원칙에 위반된다. 사실 다형성만으로는 OCP, DIP를 지킬 수 없다.
<br> **OCP 위반** : `MemberService` 는 repository source를 바꾸려면 소스수정이 필요하다. 
<br> **DIP 위반** : `MemberService` 는 `MemberRepository` 인터페이스에 의존하면서 DIP를 지킨 것 같아보이지만, 실상은 추상(MemberRepository)뿐만 아니라, 구현 클래스(MemoryMemberRepository)에도 의존하고 있는 셈이다.
<br><br> 스프링의 DI/DI container를 통하여 다형성 + OCP, DIP를 지원 !!! (클라이언트의 코드 변경없이 기능 확장가능)

#### 해결방안
> 인터페이스에만 의존하도록 코드를 변경한다. <br> 
How? 애플리케이션의 전체 동작 방식을 구성하기 위해, 구현 객체를 생성/연결하는 책임을 가지는 별도의 설정 클래스를 따로 두는 것. **생성/연결과 실행의 분리**

```java
class MemberService {

   // 인터페이스에만 의존하며 구현객체는 생성자 주입을 통해 전달받자
   MemberRepository m;

   // 생성자 주입. 해당 인터페이스의 구현객체는 MemberService의 입장에서는 알 수 없다.
   // OCP, DIP를 모두 충족한 바람직한 코드가 완성됨.
   public MemberService(MemberRepository m) {
      this.m = m;
   }
   
   ...

}

public class AppConfig {

   public MemberService memberService() {
      // Jdbc DB 사용을 위한 생성자 주입
      return new MemberService(new JdbcMemberRepository());
   }

}
```