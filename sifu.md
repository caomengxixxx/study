#### 私服

```java
1月7日
    
找不到jar包的bug可能是maven中没有配置私服地址，而那个jar包刚好就在私服中，所以需要在maven中配置一下公司的私服地址即可解决问题。（猜的）
```

#### 在maven中配置私服地址

```xml
<!-- 改成公司的私服地址即可 -->
<mirror>
	<id>public</id>
	<mirrorOf>*</mirrorOf>
	<name>public repositroy</name>
	<url>https://192.168.1.1:8080/./././</url>
</mirror>

<!-- 
	 id :  群组ID
 	 name: 介绍
     url: 组仓库的地址
	 mirrorOf: 引组里面的那些仓库，*为全部
-->
```

#### 上传项目到私服

```xml
<!-- 配置setting.xml(用户名和密码)用于上传jar包(maven中) -->
<server>
    <id>releases</id>
    <username>admin</username>
    <password>admin123</password>
</server>

<server>
    <id>snapshots</id>
    <username>admin</username>
    <password>admin123</password>
</server>

<!-- 配置pom.xml(项目中) -->
<distributionManagement>
    <!-- 上传稳定版或者发行版 -->
    <repository>
        <id>releases</id>
        <url>http://192.168.1.1:8080/././</url>
    </repository>
    <!-- 上传开发版或者发行版 -->
    <snapshotRepository>
        <id>snapshots</id>
        <url>http://192.168.1.1:8080/././</url>
    </snapshotRepository>
</distributionManagement>

<!-- 地址一定要改成公司的私服地址 -->
```

#### 从私服上引用别人的依赖

```xml
<!-- 在maven的setting.xml中配置 -->
<profile>
    <id>public</id>
    <repositories>
        <repository>
            <id>Nexus</id>
            <url>http://192.168.1.1:8080/./././</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
                <updatePolicy>always</updatePolicy>
            </snapshots>
        </repository>
    </repositories>
</profile>

<activeProfiles>
	<activeProfile>public</activeProfile>
</activeProfiles>
```

