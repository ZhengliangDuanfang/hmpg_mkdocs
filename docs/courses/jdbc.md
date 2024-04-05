!!! info "说明"
    这里是数据库系统课程lab5的开发备忘录。

[实验文档](https://www.yuque.com/yingchengjun/ozqlqv/gnwbgi9my2ci7has?singleDoc)

## JDBC笔记

整理自[CSDN](https://blog.csdn.net/fhuqw/article/details/120095166)

JDBC API主要位于java.sql包中，该包定义了一系列访问数据库的接口和类。

#### 1. Driver接口

Driver接口是所有JDBC驱动程序必须实现的接口，该接口专门提供给数据库厂商使用。需要注意的是，在编写JDBC程序时，必须要把所使用的数据库驱动程序或类库加载到项目的classpath中(这里指MySQL驱动JAR包)。

#### 2. DriverManager接口

DriverManager接口用于加载JDBC驱动、创建与数据库的连接。在DriverManager接口中，定义了两个比较重要的静态方法。

| 方法名称                                                     | 功能描述                                             |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| static void registerDriver(Driver driver)                    | 用于向DriverManager注册给定的JDBC驱动程序            |
| static Connection getConnection(String url,String user,String pwd) | 用于建立和数据库连接，并返回表示连接的Connection对象 |

#### 3.Connection接口

Connection接口用于处理与特定数据库的连接，Connection对象是表示数据库连接的对象，只有获得该连接对象，才能访问并操作数据库。Connection接口的常用方法如下表。

| 方法名称                                       | 功能描述                                                     |
| ---------------------------------------------- | ------------------------------------------------------------ |
| Statement createStatement()                    | 用于创建一个Statement对象将SQL语句发送到数据库               |
| PreparedStatement prepareStatement(String sql) | 用于创建一个PreparedStatement对象将参数化的SQL语句发送到数据库 |
| CallableStatement prepareCall(String sql)      | 用于创建一个CallableStatement对象来调用数据库存储过程        |

#### 4.Statement接口

Statement接口用于执行静态的SQL语句，并返回一个结果对象。Statement接口对象可以通过Connection实例的createStatement()方法获得，该对象会把静态的SQL语句发送到数据库中编译执行，然后返回数据库的处理结果。

Statement接口提供了3个常用的执行SQL语句的方法。

| 方法名称                           | 功能描述                                                     |
| ---------------------------------- | ------------------------------------------------------------ |
| boolean execute(String sql)        | 用于执行各种SQL语句。该方法返回一个boolean类型的值。如果为true，表示所执行的SQL语句有查询结果，可以通过Statement的getResultSet()方法获得查询结果。 |
| int executeUpdate(String sql)      | 用于执行SQL中的insert、update、delete语句。该方法返回一个int类型的值，表示数据库中受该SQL语句影响的记录条数。 |
| ResultSet executeQuery(String sql) | 用于执行SQL中的select语句。该方法返回一个表示查询结果的ResultSet对象。 |

#### 5.PreparedStatement接口

Statement接口封装了JDBC执行SQL语句的方法，可以完成Java程序执行SQL语句的操作。然而在实际开发过程中往往需要将程序中的变量作为SQL语句的查询条件，而使用Statement接口操作这些SQL语句会过于繁琐，并且存在安全方面的问题。针对这一问题，JDBC API提供了扩展的PreparedStatement接口。

PreparedStatement接口提供了一些常用方法，如下表。

| 方法名称                                    | 功能描述                                                     |
| ------------------------------------------- | ------------------------------------------------------------ |
| int executeUpdate()                         | 在PreparedStatement对象中执行SQL语句必须是一个DML语句或者是无返回内容的SQL语句，如DDL语句。 |
| ResultSet executeQuery()                    | 在PreparedStatement对象中执行SQL查询，该方法返回的是ResultSet对象。 |
| void setInt(int parameterIndex,int x)       | 将指定参数设置给定的int值。                                  |
| void setString(int parameterIndex,String x) | 将指定参数设置成给定的String值。                             |

应用举例：

```sql
PreparedStatement pStmt = conn. prepareStatement ("insert into instructor values(?,?,?,?)");
pStmt.setString (1, "88877");
pStmt.setString (2, "Perry");
pStmt.setString (3, "Finance");
pStmt.setInt (4, 125000);
pStmt.executeUpdate();
pStmt.setString (1, "88878");
pStmt.executeUpdate();
```

#### 6.ResultSet接口

ResultSet接口用于保存JDBC执行查询时返回的结果集，该结果集封装在一个逻辑表格中。在ResultSet接口内部有一个指向表格数据行的游标(或指针)，ResultSet对象初始化时，游标在表格第一行之前，调用next()方法可以将游标移动到下一行。如果下一行没有数据，则返回false。在应用程序中经常使用next()方法作为while循环的条件来迭代ResultSet结果集。

ResultSet接口的常用方法如下表。

| 方法名称                            | 功能描述                                                     |
| ----------------------------------- | ------------------------------------------------------------ |
| String getString(int columnIndex)   | 用于获取指定字段的String类型的值，参数columnIndex代表字段的索引。 |
| String getString(String columnNmae) | 用于获取指定字段的String类型的值，参数columnIndex代表字段的索引。 |
| int getInt(int columnIndex)         | 用于获取指定字段的int类型的值，参数columnIndex代表字段的索引。 |
| int getInt(String columnName)       | 用于获取指定字段的int类型的值，参数columnName代表字段的名称。 |
| boolean next()                      | 将游标从当前位置向下移一行。                                 |

