### 常用命令
```
gradle build #编译    
gradle bootrun #运行

```

### Mac安装Gradle
```
sudo port install gradle   
```

### Spring boot CLI
```
sudo port install spring-boot-cli    
mkdir demo   
cd demo   
spring init -d=web -g=com.example -a=demo --package-name=com.example --name=demo -x
```
```
-d（dependencies 依赖包）   
-g（Group Id）   
-a（Artifact Id）   
–package-name（Package name）   
–name（Project name）   
-x（Extract compatible archives）   

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
sts > Spring tools

```

### 解决 Gradle does not find tools.jar 问题
```
export JAVA_HOME=/Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin/Contents/Home   
修改为
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home  

```

### 解决com.example.demo.DemoApplicationTests > initializationError FAILED java.lang.IllegalStateException 问题
```
注释掉 src/test/com/example/demo/DemoApplicationTests 中的代码   
```

### 参考网址
[Spring Boot MVC Example](http://www.technicalkeeda.com/spring-tutorials/spring-boot-mvc-example)    
[使用Gradle创建一个最简单的Spring Boot项目](http://blog.csdn.net/u013360850/article/details/53415005)
[eclipse下SpringBoot开发和测试](http://somefuture.iteye.com/blog/2247207)
[Spring Boot集成Groovy混合Java开发](http://www.bijishequ.com/detail/369614?p=)
[Spring Initializr](http://start.spring.io/)   
[Spring Boot Reference Guide](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#getting-started-installing-the-cli)   
[重拾后端之Spring Boot](http://www.jianshu.com/p/4e25e25b62c2)
[spring-boot 入门](http://blog.csdn.net/qq_31655965/article/details/71258333)

### 事物回滚
```
@Autowired
private TransactionTemplate transactionTemplate;

方法体中插入
int rs=transactionTemplate.execute(new TransactionCallback<Integer>() {

				@Override
				public Integer doInTransaction(TransactionStatus status) {
					new ResultObject(
							db.table("base", "student_").insert(map)>0
							,"录入成功"
							,"录入失败"
							).toJson();
					status.setRollbackOnly();
					return 2;
				}
			});

```
