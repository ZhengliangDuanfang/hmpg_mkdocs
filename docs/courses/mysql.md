!!! info "说明"
    这里记录一些在课上知识之外但是会用到的MySQL知识。


## MySQL 基本操作

`win+R`然后输入`mysqlsh`进入MySQL Shell。

### MySQL的登录与退出

在MySQL Shell的JS模式下：
```Shell
\connect −h localhost −P 3306 −u root −p
# 按提示输入密码
\sql
# 进入后，通过ctrl + D 退出
```

在Windows PowerShell中：
```Shell
mysql −h localhost −P 3306 −u root −p
# 按提示输入密码
# 进入后，通过运行exit; 或者quit; 语句退出
```

SQL或者JS模式下，都可以直接\exit退出。

### 用户操作

#### 创建用户

这句需要在已经登陆后执行。
```SQL
create user '用户名'@'主机名' identified by '密码';
```
注意都要加单引号。

新创建的用户只有登录 MySQL 服务器的权限，没有任何其它权限。

#### 查询用户表

```SQL
select user, host, password from mysql.user;
```

#### 查询用户权限

```SQL
show grants for '用户名'@'主机名';
```

#### 删除用户

```SQL
drop user '用户名'@'主机名';
```
这个主机名可以直接填'%'代表与任何都匹配。

### 对数据库的操作

#### 创建数据库

```SQL
create schema <名称>;
```

#### 查询数据库

```SQL
show schemas;
```

#### 进入数据库

```SQL
use <名称>;
```

#### 删除数据库

```
drop schema <名称>;
```

## MySQL Trigger

需要前后套`delimeter $$ $$`来防止分号提前结束输入。
此外与课件中不同的是，没有`referencing new/old row as xxx`这一行；用if-else语句代替when。

举例：

```SQL
delimiter $$
create trigger invalid_year before update on teaches
for each row
begin
    if (new.year < 1900) then
        set new.year = null;
    end if;
end; $$
delimiter ;
```

## MySQL 模糊查找

使用`SOUNDEX(string)`函数。

请参考 [https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_soundex](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_soundex)

