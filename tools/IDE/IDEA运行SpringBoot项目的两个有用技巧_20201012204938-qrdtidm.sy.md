![](https://b3logfile.com/bing/20200511.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)

# 前言

本篇文章主要记录一下在IDEA中运行SpringBoot项目的一些技巧，主要包括两个，第一个小技巧：以不同端口号同时行同一个SpringBoot项目；第二个小技巧，将多个SpringBoot项目运行在services界面，这样更加方便管理。

# 创建一个SpringBoot项目

我们需要要创建一个SpringBoot项目，用这个项目来演示。创建过程很简单，在IDEA中，依次点击Fiel -> New -> Project 然后进入下面的界面即可创建SpringBoot项目了

![springbootdemo.png](https://b3logfile.com/file/2020/10/springbootdemo-76ed42b2.png)

创建完成后，在配置文件`application.yml`中增加如下配置

```
server:
  port: 8080
```

并且在`pom.xml`中引入`web`依赖

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

在启动类中增加一些代码：

```
@SpringBootApplication
@RestController
public class SpringbootDemoApplication {

    @Value("${server.port}")
    String port;

    @RequestMapping("/hello")
    public String hello() {
        return "hello, i am from port: " + port;
    }

    public static void main(String[] args) {
        SpringApplication.run(SpringbootDemoApplication.class, args);
    }

}
```

# 小技巧一：以不同的端口号同时运行同一个SpringBoot项目

我们已经创建好`springboot-demo`这个项目了，下面开始演示如何以多个端口号同时运行它

### 第一步

点击右上方的`Edit Configurations`按钮

![clickedit.png](https://b3logfile.com/file/2020/10/clickedit-9381db60.png)

### 第二步

我们会进入下面这个界面，点击右上角的`Allow parallel run`前面的框框，然后再点击左侧的复制按钮

![allowparallelrunandcopy.png](https://b3logfile.com/file/2020/10/allowparallelrunandcopy-915e2fa4.png)

### 第三步

经过第二步我们会进入下面这个界面，将name改为SpringbootDemoApplication2，然后在VM options这里填入`-Dserver.port=8081`

![application2.png](https://b3logfile.com/file/2020/10/application2-f8e1b310.png)

### 第四步

重复第二第三步的操作，在创建一个以8082端口运行的模板SpringbootDemoApplication3，我们就可以看到如下所示的效果，然后依次运行它们

![three.png](https://b3logfile.com/file/2020/10/three-3d896ea7.png)

### 第五步

运行成功后，打开浏览器

访问 [http://localhost:8080/hello](http://localhost:8080/hello)，返回`hello, i am from port: 8080`访问 [http://localhost:8081/hello](http://localhost:8081/hello)，返回`hello, i am from port: 8081`访问 [http://localhost:8082/hello](http://localhost:8082/hello)，返回`hello, i am from port: 8082`

至此大功告成！

# 小技巧二：将多个SpringBoot项目运行在services管理界面

我们接着上面的步骤来，刚才我们创建了一个名为`springboot-demo`的项目，并且分别以8080,8081,8083这三个端口号运行起来了，Debug界面如下所示：

![debugwindows.png](https://b3logfile.com/file/2020/10/debugwindows-40baeb5d.png)

这三个Debug界面看起来不是很美观，现在我们使用service界面来管理

### 第一步

按住`Alt + 8`快捷键打开services界面

![servicewindows.png](https://b3logfile.com/file/2020/10/servicewindows-16f48e95.png)

### 第二步

依次点击Add Service -> Add Configuration Type， 然后进入下面的界面后，选择SpringBoot

![serviceselectspringboot.png](https://b3logfile.com/file/2020/10/serviceselectspringboot-1d23bb49.png)

### 第四步

然后就可以看到，我们之前添加的三个运行模板都在这里了

![service3.png](https://b3logfile.com/file/2020/10/service3-d79936f5.png)

### 第五步

运行它们

![service4.png](https://b3logfile.com/file/2020/10/service4-350b2944.png)

# 最后

这两个小技巧，在运行微服务项目时会很有用
