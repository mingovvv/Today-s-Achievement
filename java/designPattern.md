# 디자인 패턴(Design Pattern)
> 시대를 거쳐 검증된 프로그래밍 패턴. GoF(Gang of Fout)라 불리는 4명의 사람들에 의해 
> 소프트웨어 개발 영역에서 디자인 패턴이 구체화되고 체계화 되었다.  

패턴 종류
1) 생성 패턴
    1. 추상팩토리 패턴
    2. 빌더 패턴
    3. 팩토리 메서드 패턴
    4. 싱글톤 패턴 
2) 구조 패턴
    1. 어댑터 패턴
    2. 브리지 패턴
    3. 컴포지트 패턴
    4. 데코레이터 패턴
    5. 파사드 패턴
    6. 프록시 패턴
    7. 플라이웨이트 패턴
3) 행위 패턴
    1. 책임 연쇄 패턴
    2. 반복자 패턴
    3. 중재자 패턴
    4. 전략 패턴
    5. 커맨드 패턴
    6. 방문자 패턴
    7. 인터프리터 패턴
    8. 메멘토 패턴
    9. 옵저버 패턴
    10. 상태 패턴
    11. 템플릿 메소드 패턴
    12. 널 오브젝트 패턴


## 빌더 패턴(Builder Pattern)
> 빌더 패턴은 객체를 생성할 때 패턴이다. 신입때 사내 프로젝트를 뒤적거리면서 처음 접했던 디자인 패턴이였다.
생성자로 너무 많은 인자가 넘겨지는 경우 어떠한 인자가 어떠한 값을 나타내는지 확인하기 힘들다. 그로 인해 생겨난 디자인 패턴.

```
public class Student {
    private long id;
    private String name;
    private String major;
    private int age;
    private String address;
    private String gender;
    private String phone;

    public Student(long id, String name, String major, int age, String address, String gender, String phone) {
        this.id = id;
        this.name = name;
        this.major = major;
        this.age = age;
        this.address = address;
        this.gender = gender;
        this.phone = phone;
    }
}

```

```
public static void main(String[] args) {
    Student s = new Student(1,"park", "math", 30, "서울", "남자", "010-000-0000");
}
```
  
```
public static class Builder {
        // 필수
        private final long id;
        private final String name;
        private final String major;
        
        // 선택
        private int age;
        private String address;
        private String gender;
        private String phone;

        public Builder(long id, String name, String major) {
            this.id = id;
            this.name = name;
            this.major = major;
        }
        
        public Builder age(int age){
            this.age = age;
            return this;
        }
        
        ...
    }
```

##### 출처
https://jdm.kr/blog/217