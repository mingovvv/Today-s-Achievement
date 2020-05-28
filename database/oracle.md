# Oracle 관련 모음
> Oracle 데이터베이스 문법에 대한 정리

#### TO_CHAR
    TO_CHAR(SYSDATE, 'YYYY-MM-DD HH24MISS')
  - 날짜를 문자형으로 변환
  - date 타입의 날짜형태를 string 타입으로 비교할 때 사용 
#### TO_DATE
    TO_DATE('20200528', 'YYYY-MM-DD HH24MISS')
  - 문자를 날짜형으로 변환
  - string 타입의 날짜형태를 date 타입으로 비교할 때 사용
