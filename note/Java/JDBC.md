# JDBC

## JDBC使用一种与普通URL类似的语法来描述数据源

- 一般语法：jdbc:subprotocol:oher stuff
- subprotocol用于选择链接到数据库的具体驱动程序
- other stuff根据不同驱动而格式不同

## 流程

1. 下载驱动程序的JAR文件
2. 启动数据库
3. 注册驱动器类
    - 在java程序中加载驱动器类 ```Class.forName("com.mysql.jdbc.Driver")```
    - 设置jdbc.drivers属性
4. 连接数据库，得到Connection对象
    String url = "jdbc:mysql://localhost:3306/jdbc";  
    String user = "root";  
    String password = "";  
    Connection conn = DriverManager.getConnection(url, user, password); 
5. 利用Connection对象的createStatement()方法创建Statement对象
6. 利用Statement对象的executeQuery方法执行SQL语句，并保存在ResultSet中
7. 通过ResultSet的next()方法，遍历查询结果。
8. 按照顺序依次释放资源

## 代码示例

```Java
// 1.注册驱动  
Class.forName("com.mysql.jdbc.Driver");// 推荐方式  
// 2.建立连接  
String url = "jdbc:mysql://localhost:3306/jdbc";  
String user = "root";  
String password = "";  
Connection conn = DriverManager.getConnection(url, user, password);
// 3.创建语句  
Statement st = conn.createStatement(); 
// 4.执行语句  
ResultSet rs = st.executeQuery("select * from user");
// 5.处理结果  
while (rs.next()) {  
System.out.println(rs.getObject(1) + "/t" + rs.getObject(2) + "/t"  + rs.getObject(3) + "/t" + rs.getObject(4));  
}  
// 6.释放资源  
rs.close();  
st.close();  
conn.close();
```

## 预备语句（prepared statement）的使用

```Java
String sql = "select * from people p where p.id = ? and p.name = ?";  
preparedstatement ps = connection.preparestatement(sql);  
ps.setint(1,id);  
ps.setstring(2,name);  
resultset rs = ps.executequery();
```

## 存储过程调用

```Java
CallableStatement cs=null;  
//调用update存储过程  
cs=conn.prepareCall("{call pro_update_age_by_birthday(?,?)}");  
cs.setString(1, "1996-02-26");  
cs.setInt(2, 22);
cs.execute();//将生日为1996-02-26的记录，年龄更新为22岁
```
