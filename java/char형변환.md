# char형 int형으로 변환하기
> 숫자와 문자가 포함된 String형을 각 자리수로 잘게 쪼개는 작업을 하다가 적어보는 내용.

> char - '0'을 이용하면 아스키코드값을 알 필요없이 int형으로 변환 가능
> Character.getNumericValue(input.charAt(i)) 방법을 이용해도 형변환이 가능하다.

#### 변환 X
    String text = 1a2b3c;
    
    // num 값 : 아스키코드의 숫자 1을 의미하는 49가 대입
    int num = text.chartAt(0);

####  -'0' 방법
    String text = 1a2b3c;
    
    // num2 값 : 실제 1이 대입
    int num2 = text.chartAt(0) - '0';
    
#### Character.getNumericValue(val) 방법
    String text = 1a2b3c;
    
    // num2 값 : 실제 1이 대입
    int num2 = Character.getNumericValue(text.charAt(0));