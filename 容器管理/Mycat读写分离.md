# Mycat读写分离



**部署主从MySQL**

master

```
docker run -d -p 3306:3306 \
  --name mysql_master \
  -e MYSQL_DATABASE=web \
  -e MYSQL_USER=web \
  -e MYSQL_PASSWORD=web \
  -e MYSQL_ROOT_PASSWORD=root_password \
  -e MYSQL_REPLICATION_USER=user_for_slave \
  -e MYSQL_REPLICATION_PASSWORD=user_password_for_slave \
  mishamx/mysql:5.7
```



slave

```
docker run -d -p 3307:3306  \
  --name mysql_slave \
  -e MYSQL_MASTER_HOST=mysql_master \
  -e MYSQL_MASTER_PORT=3306 \
  -e MYSQL_ROOT_PASSWORD=root_password \
  -e MYSQL_REPLICATION_USER=user_for_slave \
  -e MYSQL_REPLICATION_PASSWORD=user_password_for_slave \
  --link mysql_master:mysql_master \
  mishamx/mysql:5.7
```



部署**Mycat**

下载Mycat

http://dl.mycat.org.cn/1.6.6.1



运行openjdk容器

```
docker run -p 9066:9066 -p 8066:8066 --name mycat -v E:\docker\mycat:/mycat -itd adoptopenjdk/openjdk8
```



配置Mycat账号（mycat/conf/server.xml）

```xml
<user name="root" defaultAccount="true">
    <property name="password">root1234</property>
    <property name="schemas">web</property>
</user>
```



配置Mycat逻辑库（mycat/conf/schema.xml）

```xml
<?xml version="1.0"?>
<!DOCTYPE mycat:schema SYSTEM "schema.dtd">
<mycat:schema xmlns:mycat="http://io.mycat/">

	<schema name="web" checkSQLschema="false" sqlMaxLimit="100">
		<table name="user" primaryKey="id" type="global" dataNode="dn1" />
	</schema>
	
	<dataNode name="dn1" dataHost="localhost1" database="web" />
	
	<dataHost name="localhost1" maxCon="1000" minCon="10" balance="0"
			  writeType="0" dbType="mysql" dbDriver="native" switchType="1"  slaveThreshold="100">
		<heartbeat>select user()</heartbeat>
		<writeHost host="172.17.0.3" url="172.17.0.3:3306" user="root"
				   password="root1234">
			<readHost host="172.17.0.4" url="172.17.0.4:3306" user="root" password="root1234" />
		</writeHost>
	</dataHost>

</mycat:schema>
```



启动Mycat

mycat/bin/startup_nowrap.sh