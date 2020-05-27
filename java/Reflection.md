# 자바 리플렉션(Java Reflection)
> 리플렉션이란 구체적인 클래스 타입을 알지 못해도, 객체를 통해 클래스의 정보를 분석해서 
> 그 클래스의 메소드, 타입, 변수들을 접근할 수 있도록 도와주는 자바 API를 의미한다.
> 이미 로딩이 완료된 클래스에서 또 다른 클래스를 동적으로 로딩(Dynamic Loading)하여 생성자(Constructor),
> 멤버 필드(Member Variables) 그리고 멤버 메서드(Member Method) 등을 사용할 수 있도록 한다.
> 즉, 컴파일 시간(Compile Time)이 아니라 실행 시간(Run Time)에 동적으로 특정 클래스의 정보를 객체화를 통해 분석 및 추출해낼 수 있는 프로그래밍 기법이라고 표현할 수 있다.

#### 메소드
 - class.getSuperClass() : 슈퍼 클래스를 반환
 - class.getClass() : 상속된 클래스를 포함하여 모든 공용 클래스, 인터페이스 및 열거형을 반환
 - class.getDeclaredClass() : 명시적으로 선언된 모든 클래스 및 인터페이스, 열거형을 반환
 - class.getDeclaringClass() : 클래스에 구성된 클래스(명시적으로 선언된)를 반환
 - class.getEnclosingClass() : 클래스의 즉시 동봉된 클래스를 반환