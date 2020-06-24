# ELK Stack 기본
> ElasticSearch, Logstach, Kibana, Filebeats

## ElasticSearch
 - index + type + document
 - REST API를 통해 데이터를 조회, 수정, 생성, 삭제
 - Elasticsearch: Apache Lucene을 기반으로 개발한 실시간 분산형 RESTful 검색 및 분석 엔진 
 - Logstash: 각종 로그를 가져와서 JSON 형태로 만들어 Elasticsearch로 데이터를 전송함 
 - Kibana: Elasticsearch에 저장된 데이터를 사용자에게 Dashboard 형태로 보여주는 시각화 솔루션
 - Filebeat: 로그 파일을 경령화시켜서 Elasticsearch 또는 Logstash로 넘겨주는 역할을 수행함. 특히, Logstash가 과부하되면 넘기는 속도를 줄여주고, 시스템 가동이 중단되거나 다시 시작해도, 로그의 중단점을 기억하고 그 지점부터 다시 보낼 수 있음
   
   

#### 관계형 데이터베이스와 비교
|elasticsearch|relational DB|
|------|-------|
|Index|Database|
|Type|Table|
|Document|Row|
|Filed|Column|
|Mapping|Schema|

## Logstash
 - 로그정보를 수집하여 하나의 저장소에 출력
 - 실시간 파이프라인 기능을 갖춘 데다 널리 사용되고 있는 시스템
 - 다양한 입력차원에서 데이터를 수집 및 분석, 가공 및 통합해 다양한 목적지에 저장하는 파이프라인을 쉽게 구축할 수 있음
 - Input -> Filter(전처리) -> Output

#### 참고문헌
 - https://yongho1037.tistory.com/743
 
   