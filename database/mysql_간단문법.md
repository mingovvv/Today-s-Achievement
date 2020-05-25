# MySQL 관련 모음
> MySQL 데이터베이스 문법에 대한 정리

#### CASE
    CASE 
        WHEN 조건
        THEN '반환값'
        WHEN 조건
        THEN '반환값'
        WHEN 조건
        THEN '반환값'
        ELSE '모든 조건에 해당되지 않는 경우 반환값'
 - WHEN과 THEN은 한 쌍
 - WHEN과 THEN은 다수가 존재할 수 있다.
 - ELSE가 존재하지 않고 조건에 맞지 않는다면 NULL을 반환한다.
#### IF
    IF(조건, expr1, expr2)
 - 조건이 TRUE일 경우 expr1을 리턴하고, FALSE일 경우 expr2를 리턴한다.
#### IFNULL
    IFNULL(expr1, expr2)
 - exp1이 NULL이면 exp2를 리턴하고, NULL이 아니면 exp1을 리턴한다.

#### NULLIF
    NULLIF(expr1, expr2)
 - expr1 == expr2가 True이면 NULL을 리턴하고, 그렇지 않으면 expr1을 리턴한다.