# CDATA 사용법
> `Characher Date`, 파싱하지 않은 문자 데이터  
> Mybatis 사용시, xml에 쿼리문를 작성하는데 종종 <!CDATA[...]]> 문구를 발견할 수 있다.
> 해당 문구는 `<`, `>`, `&` 등의 문자를 파싱하지 않고 그대로 출력하기 원할 때 사용한다.

즉, XML Parser를 거치지 않고 문자열로 처리하도록 만든다.
```
SELECT *
    FROM
    MEMBER
<![CDATA[
    WHERE age > 20
]]>
```
`age > 20`에서 `>`를 문자열로 인식한다.