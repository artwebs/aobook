### 常用命令
```
gradle build #编译    
gradle bootrun #运行

```

### Mac安装Gradle
```
sudo port install gradle   
```

### Quick start Spring CLI example
```
@RestController
class ThisWillActuallyRun {
    @RequestMapping("/")
    String home() {
        "Hello World!"
    }
}   
```
```
spring run app.groovy   
```
访问[localhost:8080](http://localhost:8080)


### 安装eclipse Gradle 插件
```
打开 Help > Eclipse Marketplace   
buildship > Buildship Gradle Integration   
gradle > Gradle IDE Pack 3.8.x+1.x

```

### 解决 Gradle does not find tools.jar 问题
```
export JAVA_HOME=/Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin/Contents/Home   
修改为
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home  

```

### 参考网址
[Spring Boot MVC Example](http://www.technicalkeeda.com/spring-tutorials/spring-boot-mvc-example)    
[使用Gradle创建一个最简单的Spring Boot项目](http://blog.csdn.net/u013360850/article/details/53415005)
[eclipse下SpringBoot开发和测试](http://somefuture.iteye.com/blog/2247207)
[Spring Boot集成Groovy混合Java开发](http://www.bijishequ.com/detail/369614?p=)
[Spring Initializr](http://start.spring.io/)   
[Spring Boot Reference Guide](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#getting-started-installing-the-cli)   
