# DB 커넥션 풀
> 웹 어플리케이션을 지탱하는 WAS에서 DB 서버에 접근을 시작하고 데이터를 가져오기까지의
> 단계에서 가장 많은 비용이 드는 부분은 어디일까?

```
String driverPath = "net.sourceforge.jtds.jdbc.Driver";
String address = "jdbc:jtds:sqlserver://IP/DB";
String userName = "user";
String password = "password";

String query = "SELECT ... where id = ?";
try {
 Class.forName(driverPath);
 Connection con = DriverManager.getConnection(address, userName, password);
 PreparedStatement ps = con.prepareStatement(query);
 ps.setString(1, id);
 ResultSet rs = get.executeQuery();
 // ....
} catch (Exception e) { }
} finally {
 rs.close();
 ps.close();
}
```
위 코드를 분석해보면,
1. DB 서버 접속을 위해 JDBC 드라이버를 로드한다.
2. DB 서버 접속 정보와 `DriverManager.getConnection()` 메소드를 통해 DB Connection 객체를 얻는다.
3. `Connection` 객체로부터 쿼리를 수행하기 위한 `PreparedStatement` 객체를 받는다.
4. `executeQuery()`를 수행하여 `ResultSet` 객체를 받아서 데이터를 처리한다.
5. 처리가 완료되면 처리에 사용된 리소스들을 `close()` 한다.

위의 과정에서 가장 시간이 오래 잡아먹는 부분은 2. DB Connection 객체를 얻는 부분이다.

웹 애플리케이션은 HTTP 요청에 따라 쓰레드가 생성되고 해당 쓰레드는 DB서버와 통신을 한 뒤 데이터를 
얻게 된다. 모든 요청이 DB Connection 객체를 얻는 과정을 거친다면 ?? 안봐도 뻔하다..

우리는 이런 문제를 해결하기 위해 `DBCP`(Database Connection Pool)를 이용할 수 있다.

#### DBCP
DBCP의 역할은 WAS가 실행되면서 미리 일정량의 DB Connection 객체를 생성하고 Pool이라는 공간에 저장을 한다.
HTTP 요청에 따라 필요할 때 Pool에서 Connection 객체를 가져다 쓰고 반환하며 Connection 객체를 생성하는 비용을
절약하는 방식이다.
