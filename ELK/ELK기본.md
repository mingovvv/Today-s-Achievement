# ELK Stack 기본
> ElasticSearch, Logstach, Kibana, Filebeats

## elasticsearch
 - index + type + document
 - REST API를 통해 데이터를 조회, 수정, 생성, 삭제
 - Elasticsearch: Apache Lucene을 기반으로 개발한 실시간 분산형 RESTful 검색 및 분석 엔진 
 - Logstash: 각종 로그를 가져와서 JSON 형태로 만들어 Elasticsearch로 데이터를 전송함 
 - Kibana: Elasticsearch에 저장된 데이터를 사용자에게 Dashboard 형태로 보여주는 시각화 솔루션
 - Filebeat: 로그 파일을 경령화시켜서 Elasticsearch 또는 Logstash로 넘겨주는 역할을 수행함. 특히, Logstash가 과부하되면 넘기는 속도를 줄여주고, 시스템 가동이 중단되거나 다시 시작해도, 로그의 중단점을 기억하고 그 지점부터 다시 보낼 수 있음
   
   

## 관계형 데이터베이스와 비교
|elasticsearch|relational DB|
|------|-------|
|Index|Database|
|Type|Table|
|Document|Row|
|Filed|Column|
|Mapping|Schema|

## kibana 매니지먼트
 - 