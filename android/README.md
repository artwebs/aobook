### org.apache.httpcomponents 引用问题
Warning:WARNING: Dependency org.apache.httpcomponents:httpclient:4.5.2 is ignored for debug as it may be conflicting with the internal version provided by Android.
注释掉
```
compile 'org.apache.httpcomponents:httpclient:4.5.2'
```  

### 解决安装后出现多个图标问题
注释掉以下library模块的AndroidManifest.xml以下内容

```
<!--<intent-filter>-->
               <!--<action android:name="android.intent.action.MAIN"/>-->
                <!--<category android:name="android.intent.category.LAUNCHER"/>-->
<!--</intent-filter>-->
```

### 常用链接
[用Gradle 构建你的android程序-依赖管理篇](http://www.cnblogs.com/youxilua/archive/2013/05/22/3092657.html)    