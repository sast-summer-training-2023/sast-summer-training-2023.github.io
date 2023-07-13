# 数据库 & SQL

:cheese_wedge: 前置知识：无

:mortar_board: 讲师：刘铠铭 @kaiming

:date: 日期：7 月 14 日星期五

---

在过去的一年中，我们接触的往往只有少量、临时的数据，因此数据可以以简单的文件形式直接进行存储。但随着数据的迅速膨胀，以文件存储数据的方式存在诸如可扩展性差、无法保证数据的完整性、一致性以及安全性等问题，因此数据库管理系统应运而生。而 SQL 作为当今管理数据库最常用的语言，也值得我们进行学习。

通过本节课，你将了解数据库技术的相关知识，并初步掌握利用 SQL 进行数据库管理与查询的基本方法。在小学期与软件工程课程中，本节课的所学也将得以应用。

## 课前准备

在本课程中，我们将使用 MySQL 这一关系型数据库管理系统。

### 1. 环境配置

#### 1.1 Ubuntu / Ubuntu (WSL 2)

##### 必选项

直接使用 apt 包管理器进行安装即可：

```shell
sudo apt update
sudo apt upgrade
sudo apt install mysql-server
```

之后检验是否成功安装：

```
mysql --version
```

若该步未成功运行，你可能需要使用 `service/systemctl` 来启动 `mysql` 服务。

##### 可选项

> 注：尽管该步骤并非必要，但建议你尝试手动配置以体验生产环境。
>
> 在开始前，请首先设置 root 用户密码：
>
> ```shell
> sudo mysql
> mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'YourPassword';
> 
> # 在后续操作时，即可通过 mysql -u root -p 以 root 身份登录
> ```

在生产环境中，为了提高 MySQL 的安全性，我们有必要进行安全配置，可使用如下指令进行操作：

```shell
sudo mysql_secure_installation
```

该步骤中将进行如下操作（输入指令后即可明白一切）：

- 移除不需要的默认用户（例如 root）；
- 为 root 用户设置密码，确保只有授权用户可以访问数据库；
- MySQL 在安装后会自动创建一个无用户名无密码的匿名用户 (Anonymous Account)，默认情况下 MySQL 允许匿名用户连接到数据库服务器，以方便新用户快速上手。然而在生产环境中攻击者可能利用这个漏洞来尝试访问数据库并进行恶意操作，因此我们可以在该步骤中删除匿名用户；
- 禁止远程 root 登录，限制其只能在本地访问；
- 删除测试数据库：删除 MySQL 安装过程中创建的一些测试数据库。

#### 1.2 Windows & macOS

> 注：未测试

- 在 [官网](https://dev.mysql.com/downloads/installer/) 安装 MySQL Installer，手动安装即可。
- 可参考 [网络教程](https://www.sjkjc.com/mysql/install-on-macos/)。

### 2. 用户设置

> 您无需特别在意本节代码含义，如希望提前研究可参考：
>
> - [这篇博客](https://blog.csdn.net/aiwangtingyun/article/details/106011258)
> - [MySQL :: MySQL 8.0 Reference Manual :: 13.7.1.6 GRANT Statement](https://dev.mysql.com/doc/refman/8.0/en/grant.html)

#### 2.1 创建用户

首先我们创建一个 admin 用户：

```shell
sudo mysql			# 以 root 用户登录
# or
mysql -u root -p	# 以 root 用户登录
```

```mysql
mysql> CREATE USER 'admin'@'%' IDENTIFIED BY '123456';
Query OK, 0 rows affected (0.01 sec)
```

表示允许用户 `admin` 从任意 IP 以密码 `123456` 登录。

#### 2.2 权限分配

新创建的用户是没有任何权限的（`USAGE` 表示没有任何权限），我们可以使用 `SHOW GRANTS` 进行查询：

```mysql
mysql> SHOW GRANTS FOR 'admin'@'%';
+-----------------------------------+
| Grants for admin@%                |
+-----------------------------------+
| GRANT USAGE ON *.* TO `admin`@`%` |
+-----------------------------------+
1 row in set (0.00 sec)
```

为方便后续操作，我们为 admin 添加所有数据库和数据表的所有权限：

```mysql
mysql> GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%';
Query OK, 0 rows affected (0.02 sec)
```

#### 2.3 用户登录

使用 `exit` 语句或者使用 `Ctrl-D` 即可退出登录：

```mysql
mysql> exit
Bye
```

用命令行登录 admin：

```shell
mysql -u admin -p	# 之后输入密码即可登录
```

或者使用

```shell
mysql -u admin -p123456
```

也可直接登录，但是会在 shell 的历史记录中留下密码的明文记录，因此不推荐在服务器中使用：

```shell
cat .bash_history	# .zsh_history 等
```