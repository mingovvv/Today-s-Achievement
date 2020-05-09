mybatis

config
 -     <?xml version="1.0" encoding="UTF-8"?>
       <!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
       
       <configuration>
           <settings>
               <setting name="useGeneratedKeys" value="true"/>
               <setting name="callSettersOnNulls" value="true"/>
               <setting name="lazyLoadingEnabled" value="true"/>
               <setting name="defaultStatementTimeout" value="200"/>
               <setting name="defaultExecutorType" value="REUSE"/>
               <setting name="mapUnderscoreToCamelCase" value="true"/>
               <setting name="cacheEnabled" value="false" />
               <setting name="jdbcTypeForNull" value="NULL" />
           </settings>
       
       	<typeAliases>
               <!--typeAlias만 사용할지 package만 사용할지 하나만 사용-->
               <!--<typeAlias alias="orderReceiveError" type="com.foodtechkorea.posapi.dto.OrderReceiveErrorRequest" />-->
               <package name="com.foodtechkorea"/>
       	</typeAliases>
       
           <typeHandlers>
               <typeHandler javaType="java.sql.Timestamp"
                            handler="org.apache.ibatis.type.DateTypeHandler"/>
               <typeHandler javaType="java.sql.Time"
                            handler="org.apache.ibatis.type.DateTypeHandler"/>
               <typeHandler javaType="java.util.Date"
                            handler="org.apache.ibatis.type.DateTypeHandler"/>
           </typeHandlers>
       </configuration>
 - useGeneratedKeys
   - insert 구문의 속성중 하나인 useGeneratedKeys 를 true 로 설정한다.(기본값 false)
 - callSettersOnNulls
   - resultType으로 HashMap을 많이 사용하하는데 값이 null인 칼럼은 누락되어진 상태로 나온다.
   - 해당 이슈를 null로 나올 수 있도록 해주는 설정
 - lazyLoadingEnabled
   - JPA에만 있는줄... 알았던 지연로딩..
 - defaultStatementTimeout
   - 데이터베이스로의 응답을 얼마나 오래 기다릴지를 판단하는 타임아웃을 설정
 - 	defaultExecutorType
   - 디폴트 실행자(executor) 설정. SIMPLE 실행자는 특별히 하는 것이 없다. REUSE 실행자는 PreparedStatement를 재사용한다. BATCH 실행자는 구문을 재사용하고 수정을 배치처리한다.
 - mapUnderscoreToCamelCase
   - 전통적인 데이터베이스 칼럼명 형태인 A_COLUMN을 CamelCase형태의 자바 프로퍼티명 형태인 aColumn으로 자동으로 매핑하도록 함
 - cacheEnabled
   - 설정에서 각 매퍼에 설정된 캐시를 전역적으로 사용할지 말지에 대한 여부
 - jdbcTypeForNull
   - JDBC타입을 파라미터에 제공하지 않을때 null값을 처리한 JDBC타입을 명시한다. 일부 드라이버는 칼럼의 JDBC타입을 정의하도록 요구하지만 대부분은 NULL, VARCHAR 나 OTHER 처럼 일반적인 값을 사용해서 동작한다. 


typeAliases
 - 타입 별칭은 자바 타입에 대한 짧은 이름이다. 오직 XML 설정에서만 사용되며, 타이핑을 줄이기 위해 존재한다
 -     <typeAliases>
         <typeAlias alias="Author" type="domain.blog.Author"/>
         <typeAlias alias="Blog" type="domain.blog.Blog"/>
         <typeAlias alias="Comment" type="domain.blog.Comment"/>
         <typeAlias alias="Post" type="domain.blog.Post"/>
         <typeAlias alias="Section" type="domain.blog.Section"/>
         <typeAlias alias="Tag" type="domain.blog.Tag"/>
       </typeAliases>
  
typeHandlers
 - 마이바티스가 PreparedStatement에 파라미터를 설정하고 ResultSet에서 값을 가져올때마다 TypeHandler는 적절한 자바 타입의 값을 가져오기 위해 사용된다. 다음의 표는 디폴트 TypeHandlers를 설명한다.
 
 

링크
 - https://mybatis.org/mybatis-3/ko/configuration.html