## Mac下安装
1. [使用安装包](https://cloud.tencent.com/developer/article/1625825)
```
注意：在configure MySQL Server选项处，选择"Use Legacy Password Encryption"
```
2. 安装成功后需要配置环境变量(在.bash_profile文件添加)：
```
export PATH=${PATH}:/usr/local/mysql/bin
```
3. 随后即可在Terminal中访问mysql
```
本地访问：
mysql -u root -p
(-u 后边需要跟username，本地一般都是root；-p即为需要密码访问，随后输入密码即可)

```

Reference：
- [安装及访问](https://zhuanlan.zhihu.com/p/27960044)
- [命令行访问mysql](https://cloud.tencent.com/developer/news/371453)
- [新：homebrew安装](https://www.cnblogs.com/mybilibili/p/11604679.html#:~:text=homebrew%20安装%20mysql%20homebrew%20是%20macOS%20缺失的软件包管理器%2C譬如可以下载%20mysql、redis、wget,等等.操作系统：macOS%20High%20Sierra%20Version%2010.14.5%20Homebrew%20会将软件包安装到独立目录%2C并将其文件软链接至%20%2Fusr%2Flocal.)
- [hombrew安装启动报错](https://blog.csdn.net/u012373815/article/details/82188361)

---

## Windows
- [修改密码](https://blog.csdn.net/chouzhou9701/article/details/104786266)
```
mySQL 5.7以下user表的密码字段是“password”
```

---
## 通用
- 常用命令
```
- show databases; # check databases already existed
- use [database name]; # change current database to [database name]
- show tables; # check tables in the current database
- desc [table name]; # check the information of the target table
```

- 查看mysql端口号
```
show global variables like 'port'
```

REFERENCE:
- [查看表名和列名](https://blog.csdn.net/yelllowcong/article/details/79112029)
