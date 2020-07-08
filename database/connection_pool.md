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
2. DB 서버 접속 정보와 DriverManager.getConnection() 메소드를 통해 DB Connection 객체를 얻는다.
3. Connection 객체로부터 쿼리를 수행하기 위한 PreparedStatement 객체를 받는다.
4. executeQuery()를 수행하여 ResultSet 객체를 받아서 데이터를 처리한다.
5. 처리가 완료되면 처리에 사용된 리소스들을 close() 한다.

 ㅍ
