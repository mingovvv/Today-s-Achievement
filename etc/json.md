# JSON(JavaScript Object Notation)
> 데이터를 저장하거나 전송할 때 많이 사용되는 경량의 데이터 교환 형식.  
> 최근에는 JSON이 XML을 대체해서 데이터 전송에 많이 사용되는 추세이다.   
> 특정 언어에 종속되지 않으며, 대부분의 프로그래밍 언어에서 JSON 포맷의 데이터를 핸들링 할 수 있는 라이브러리를 제공한다.  

### JSON 문법
 - JSON은 **Key-Value**로 이루어져 있으며 String의 경우 항상 쌍 따음표로 표기된다.

       { 
            "name" : "devyu",
            "age" : 11,
            "location" : "seoul" 
        }
        
 - **객체**, **배열**을 나타낼 수 있으며, 원하는만큼 중첩이 가능하다.
 
       {
            "name" : "devyu",
            "age" : 11,
            "location" : "seoul",
            "friend" : {"name" : "ISB", "age" : 28}, // 객체
            "familly" : ["father", "mother", "sister"] // 배열
        }
        
  - JSON null 가능

### JSON과 Object
 - 라이브러리를 통해 JSON ↔ Object(객체) 사이는 변환이 가능하다.

### JSON 변환 라이브러리
[라이브러리 속도 비교](#http://www.yunsobi.com/blog/entry/java-json-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EB%B3%84-parser-%EC%86%8D%EB%8F%84-%EB%B9%84%EA%B5%90)
 - Jackson
 - Gson
 - Json.simple
 - JSONP

>spring 3.0 이후부터 Jackson과 연관된 API를 제공함으로써, Jackson라이브러리를 사용할때, 자동화 처리가 가능해 졌다. 클래스패스에 Jackson 라이브러리가 존재한다면 자동적으로 MessageConverter에 등록이 된다.   
>즉, @ResponseBody 애노테이션을 사용하여 데이터를 넘길때 Object 형태로 넘겨도 JSON 형식으로 자동변환 된다.(Getter 필요)

Getter를 사용하지 않는 데이터 매핑 방식

    // json 출력 : {"nickname":devyu"}
    public class Person {
        @JsonProperty("nickName")
        private String name = "devyu";
    }                                          


 