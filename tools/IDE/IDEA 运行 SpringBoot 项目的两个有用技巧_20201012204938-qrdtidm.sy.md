![](https://b3logfile.com/bing/20200511.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)
{: id="20201013085731-bdsfv59"}

# 前言
{: id="20201013085731-rre434z"}

本篇文章主要记录一下在IDEA中运行SpringBoot项目的一些技巧，主要包括两个，第一个小技巧：以不同端口号同时行同一个SpringBoot项目；第二个小技巧，将多个SpringBoot项目运行在services界面，这样更加方便管理。
{: id="20201013085731-d67rauc"}

# 创建一个SpringBoot项目
{: id="20201013085731-gsxy8qe"}

我们需要要创建一个SpringBoot项目，用这个项目来演示。创建过程很简单，在IDEA中，依次点击Fiel -> New -> Project 然后进入下面的界面即可创建SpringBoot项目了
{: id="20201013085731-f7b62p8"}

![springbootdemo.png](https://b3logfile.com/file/2020/10/springbootdemo-76ed42b2.png)
{: id="20201013085731-a47kdhi"}

创建完成后，在配置文件`application.yml`中增加如下配置
{: id="20201013085731-v5ilf40"}

```
server:
  port: 8080
```
{: id="20201013085731-1pk1klq"}

并且在`pom.xml`中引入`web`依赖
{: id="20201013085731-4l49pm0"}

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
{: id="20201013085731-or5k9l7"}

在启动类中增加一些代码：
{: id="20201013085731-gjqmvmd"}

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
{: id="20201013085731-04lchgk"}

# 小技巧一：以不同的端口号同时运行同一个SpringBoot项目
{: id="20201013085731-nmr3xg1"}

我们已经创建好`springboot-demo`这个项目了，下面开始演示如何以多个端口号同时运行它
{: id="20201013085731-3pkwwao"}

### 第一步
{: id="20201013085731-6dnn68m"}

点击右上方的`Edit Configurations`按钮
{: id="20201013085731-tf1f7up"}

![clickedit.png](https://b3logfile.com/file/2020/10/clickedit-9381db60.png)
{: id="20201013085731-szupfdd"}

### 第二步
{: id="20201013085731-0xivtaz"}

我们会进入下面这个界面，点击右上角的`Allow parallel run`前面的框框，然后再点击左侧的复制按钮
{: id="20201013085731-95yd91n"}

![allowparallelrunandcopy.png](https://b3logfile.com/file/2020/10/allowparallelrunandcopy-915e2fa4.png)
{: id="20201013085731-qvgj0j9"}

### 第三步
{: id="20201013085731-lkmalgv"}

经过第二步我们会进入下面这个界面，将name改为SpringbootDemoApplication2，然后在VM options这里填入`-Dserver.port=8081`
{: id="20201013085731-95gwen1"}

![application2.png](https://b3logfile.com/file/2020/10/application2-f8e1b310.png)
{: id="20201013085731-zotx6r0"}

### 第四步
{: id="20201013085731-h844zjs"}

重复第二第三步的操作，在创建一个以8082端口运行的模板SpringbootDemoApplication3，我们就可以看到如下所示的效果，然后依次运行它们
{: id="20201013085731-lymuknx"}

![three.png](https://b3logfile.com/file/2020/10/three-3d896ea7.png)
{: id="20201013085731-j2logzg"}

### 第五步
{: id="20201013085731-c5mr83f"}

运行成功后，打开浏览器
{: id="20201013085731-e01ojzz"}

访问 [http://localhost:8080/hello](http://localhost:8080/hello)，返回`hello, i am from port: 8080`访问 [http://localhost:8081/hello](http://localhost:8081/hello)，返回`hello, i am from port: 8081`访问 [http://localhost:8082/hello](http://localhost:8082/hello)，返回`hello, i am from port: 8082`
{: id="20201013085731-bgky0zk"}

至此大功告成！
{: id="20201013085731-4ph848z"}

# 小技巧二：将多个SpringBoot项目运行在services管理界面
{: id="20201013085731-7gsb39w"}

我们接着上面的步骤来，刚才我们创建了一个名为`springboot-demo`的项目，并且分别以8080,8081,8083这三个端口号运行起来了，Debug界面如下所示：
{: id="20201013085731-pkbxoil"}

![debugwindows.png](https://b3logfile.com/file/2020/10/debugwindows-40baeb5d.png)
{: id="20201013085731-gya9hz9"}

这三个Debug界面看起来不是很美观，现在我们使用service界面来管理
{: id="20201013085731-fmvldvo"}

### 第一步
{: id="20201013085731-t2p254a"}

按住`Alt + 8`快捷键打开services界面
{: id="20201013085731-guv8zqf"}

![servicewindows.png](https://b3logfile.com/file/2020/10/servicewindows-16f48e95.png)
{: id="20201013085731-ibh2frz"}

### 第二步
{: id="20201013085731-gu0t5uw"}

依次点击Add Service -> Add Configuration Type， 然后进入下面的界面后，选择SpringBoot
{: id="20201013085731-xnjdzvc"}

![serviceselectspringboot.png](https://b3logfile.com/file/2020/10/serviceselectspringboot-1d23bb49.png)
{: id="20201013085731-zm8e7rx"}

### 第四步
{: id="20201013085731-60j1nji"}

然后就可以看到，我们之前添加的三个运行模板都在这里了
{: id="20201013085731-wnhj0ab"}

![service3.png](https://b3logfile.com/file/2020/10/service3-d79936f5.png)
{: id="20201013085731-3m81sdq"}

### 第五步
{: id="20201013085731-1xga7l0"}

运行它们
{: id="20201013085731-h6ok4bs"}

![service4.png](https://b3logfile.com/file/2020/10/service4-350b2944.png)
{: id="20201013085731-udmzga4"}

# 最后
{: id="20201013085731-yaise8v"}

这两个小技巧，在运行微服务项目时会很有用
{: id="20201013085731-nw4iq8c"}
