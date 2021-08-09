**maven是用来下载依赖和打包代码的工具。**

**本章主要简单介绍maven的下载以及配置**

- 1.maven的下载
- 2.环境变量的配置
- 3.配置文件的配置
- 4.idea设置





**1.maven的下载与安装**

maven可以直接从官网下载最新的版本。

maven版本太高或者太低都会有兼容性问题，目前（2021/7）推荐使用3.3.*至3.6.*之间。其中binaries是编译好的文件，source是源代码，需要重新编译。推荐下载binaries版本。

https://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.6.3/binaries/

下载后直接解压即可，我将目录移至了C:\Program Files下，如图

![maven](C:\Users\admin\Desktop\maven.JPG)

**2.环境变量的配置**

配置maven前，需要检查Java是否已经配置。

![java](C:\Users\admin\Desktop\java.JPG)

如果没有的话，需要同时配置java和maven的环境变量

如下图，在环境变量的系统变量中添加JAVA_HOME和MAVEN_HOME,分别为安装路径

![home](C:\Users\admin\Desktop\home.JPG)

之后将java和maven的bin、路径分别添加到path中

![bin](C:\Users\admin\Desktop\bin.JPG)

win10以下版本如下图

![win7 maven](C:\Users\admin\Desktop\win7 maven.JPG)

最后在cmd中输入mvn-v ，可以正常查到即可

![maven版本](C:\Users\admin\Desktop\maven版本.JPG)



3.**配置文件的配置**

![maven](C:\Users\admin\Desktop\maven.JPG)

打开maven目录下的conf目录，

![conf](C:\Users\admin\Desktop\conf.JPG)

打开settings.xml配置仓库的本地路径和远程仓库路径。

如果不配置，那么远程仓库路径是国外路径，速度较慢；默认依赖下载路径为

C:\Users\admin\\.m2\repository

C盘用户下的repository路径。



在settings中添加

 `<localRepository>D:\repository</localRepository>`

在mirrors中添加

```java
<mirror>
        <id>alimaven</id>
        <mirrorOf>central</mirrorOf>
        <name>aliyun maven</name>
        <url>https://maven.aliyun.com/repository/central/</url>
</mirror>
```

最后结果如图

![settings](C:\Users\admin\Desktop\settings.JPG)



**4.idea设置**

idea的设定分为项目设定和全局设定，如果要每次打开idea都使用配置好的maven，在打开界面选择

Configure->Settings->Maven

Maven home directory选择设定好的版本，local repository就会自动变更，如果没有自动变更说明上一步配置文件设置错了，至此maven就已经配置好了。

![idea](C:\Users\admin\Desktop\idea.JPG)