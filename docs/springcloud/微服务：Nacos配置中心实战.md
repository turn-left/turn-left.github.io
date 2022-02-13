## 微服务：Nacos配置中心实战

#### 概述

- [Nacos官网](https://nacos.io/zh-cn/docs/what-is-nacos.html)

- [Nacos官方github](https://github.com/alibaba/nacos)

#### Nacos安装配置

1. [官网下载安装包](https://nacos.io/zh-cn/docs/quick-start.html)

2. 执行初始SQL语句

我这里Nacos解压位置D:\work2022\micro_service\nacos-server-1.4.3，进到\nacos\conf

![image-20220212140120250](/docs/springcloud/img/image-20220212140120250.png)3. 修改数据库配置 **application.properties**

```properties
### Count of DB:
db.num=1

### Connect URL of DB:
db.url.0=jdbc:mysql://127.0.0.1:3306/nacos_config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user.0=root
db.password.0=root
```

4. windows下启动 

```bash
startup.cmd -m standalone
```

如果机器内存不够，可适当调节**startup.cmd**中配置的**JVM**参数。

5. 访问控制台

- 本地默认控制台地址  http://localhost:8848/nacos/

- 默认用户 nacos/nacos



#### Nacos领域模型

- namespace
- group
- cluster
- version









#### 参考资料

- [windows如何删除无用服务](https://blog.csdn.net/gaoxin_gx/article/details/89639867)

