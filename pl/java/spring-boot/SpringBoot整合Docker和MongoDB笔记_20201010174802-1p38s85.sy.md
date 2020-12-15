![](https://b3logfile.com/bing/20190309.jpg?imageView2/1/w/960/h/540/interlace/1/q/100)

# 前言

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
一开始我只是想学一下 `Docker`，在了解了 `Docker` 的基础知识后，发现 `Docker` 安装软件很方便，于是就通过 `Docker` 安装了 `MongoDB`，顺带着把 `MongoDB` 也学习了，最后想着，既然 `Docker` 和 `MongoDB` 都学习了，为什么不顺带着将 `MongoDB` 和 `SpringBoot` 整合一下，再通过 `Docker` 部署呢？于是乎就有了这篇笔记，记录一下学习的过程。

# Docker 学习

`Docker` 的学习主要参考 [Docker 官网](https://docs.docker.com/get-started/overview/) 和 [菜鸟教程-Docker 教程](https://www.runoob.com/docker/docker-tutorial.html)

`Docker` 的安装以及 一些基础的知识，包括 **镜像** 和 **容器** 等概念，看一下 [Docker 官网](https://docs.docker.com/get-started/overview/)就可以 。需要熟练使用 **镜像** 和 **容器**  的操作指令，包括拉取（删除、打包。 镜像，运行（停止、删除）容器等。这些指令和 `git` 和 `Linux` 的指令很像的，很容易掌握。总结如下：

### 镜像操作指令

以 `Docker` 官网提供的 `hello-world` 镜像为例
=======
一开始我只是想学一下`Docker`，在了解了`Docker`的基础知识后，发现`Docker`安装软件很方便，于是就通过`Docker`安装了`MongoDB`，顺带着把`MongoDB`也学习了，最后想着，既然`Docker`和`MongoDB`都学习了，为什么不顺带着将`MongoDB` 和 `SpringBoot`整合一下，再通过`Docker`部署呢？于是乎就有了这篇笔记，记录一下学习的过程。

# Docker 学习

`Docker`的学习主要参考[Docker官网](https://docs.docker.com/get-started/overview/) 和 [菜鸟教程-Docker教程](https://www.runoob.com/docker/docker-tutorial.html)

`Docker`的安装以及 一些基础的知识，包括 **镜像** 和 **容器** 等概念，看一下[Docker官网](https://docs.docker.com/get-started/overview/)就可以 。需要熟练使用 **镜像** 和 **容器**  的操作指令，包括拉取（删除、打包. 镜像，运行（停止、删除）容器等。这些指令和`git`和`Linux`的指令很像的，很容易掌握。总结如下：

### 镜像操作指令

以`Docker`官网提供的`hello-world`镜像为例
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

##### 1. 查找镜像

指令： `docker search hello-world`

![imagesearch.png](https://b3logfile.com/file/2020/09/imagesearch-c81ebb16.png)

##### 2. 拉取镜像

指令： `docker pull hello-world `

![imagepull.png](https://b3logfile.com/file/2020/09/imagepull-da88eb40.png)

##### 3. 列出所有镜像

指令：  `docker image ls ` 或者 `docker images`

![imagelist.png](https://b3logfile.com/file/2020/09/imagelist-92d25355.png)

##### 4. 删除镜像

指令： `docker rmi hello-world`

### 容器操作指令

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
容器的操作，就结合安装 `MongoDB` 来一起学习，`Docker` 安装软件就是将该软件对应的 `Docker` 镜像拉取下来，然后运行成为一个容器的过程。常用的开发软件都有对应的 `Docker` 镜像的，我们可以在 [DockerHub](https://hub.docker.com/search?type=image) 这个网站去找我们需要的软件镜像。比如我们搜索 `mongodb`，如下图所示：
=======
容器的操作，就结合安装`MongoDB`来一起学习，`Docker`安装软件就是将该软件对应的`Docker`镜像拉取下来，然后运行成为一个容器的过程。常用的开发软件都有对应的`Docker`镜像的，我们可以在[DockerHub](https://hub.docker.com/search?type=image)这个网站去找我们需要的软件镜像。比如我们搜索`mongodb`，如下图所示：
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

![mongodbiamge.png](https://b3logfile.com/file/2020/09/mongodbiamge-7a82ee62.png)

第一个就是我们要找的镜像，我们点进去，右侧就是我们拉取镜像的指令。

![mongofbdownload.png](https://b3logfile.com/file/2020/09/mongofbdownload-0ff13f29.png)

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
##### 1. 拉取 `MongoDB` 镜像
=======
##### 1. 拉取`MongoDB`镜像
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

指令： `docker pull mongo`

##### 2. 运行容器

指令： `docker run -itd --name mongo -p 27017:27017 mongo --auth`

参数说明：

- -i : 交互式操作
- -t : 终端
- -d : 后台运行
- --name : mongo 指定容器的名字
- -p : 指定端口号
<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
- --auth : 指的是 `MongoDB` 数据库运行后，需要密码才能访问容器服务

其实使用 `Docker` 安装 `MongoDB` 这两步就完成了。
=======
- --auth : 指的是`MongoDB`数据库运行后，需要密码才能访问容器服务

其实使用`Docker`安装`MongoDB`这两步就完成了。
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

##### 3. 查看容器信息

指令： `docker ps -a`

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
这个指令会列出容器 ID、镜像、创建时间、状态、端口号、名称等信息，比较重要的就是 **CONTAINER ID(容器 ID)**，**NAMES(容器名称)** 这两个，我们可以通过它们来管理镜像
=======
这个指令会列出容器ID、镜像、创建时间、状态、端口号、名称等信息，比较重要的就是 **CONTAINER ID(容器ID)**，**NAMES(容器名称)** 这两个，我们可以通过它们来管理镜像
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

![dockerpsa.png](https://b3logfile.com/file/2020/09/dockerpsa-a9729271.png)

##### 4. 停止容器

指令：`docker stop  [容器ID] 或者 [容器名称]`

##### 5. 启动容器

指令： `docker start  [容器ID] 或者 [容器名称]`

##### 6. 重启容器

指令： `docker start  [容器ID] 或者 [容器名称]`

##### 7. 删除容器

指令： `docker rm -f  [容器ID] 或者 [容器名称]`

# MongoDB 学习

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
在前面我们已经通过 `Dokcer` 安装了 `MongoDB`，现在我们通过 `docker exec -it mongo mongo ` 指令进入 `MongoDB` 容器
=======
在前面我们已经通过`Dokcer`安装了`MongoDB`，现在我们通过`docker exec -it mongo mongo `指令进入`MongoDB`容器
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

![mogo1.png](https://b3logfile.com/file/2020/09/mogo1-b7ff4d9f.png)

初次进入，我们需要创建一个超级用户，执行下面的两个命令：

```
# 1. 切换到admin数据库

 use admin

# 2. 创建超级用户admin

db.createUser({
	user: 'admin',
	pwd: '123456',
	roles: [{
		role: 'userAdminAnyDatabase',
		db: 'admin'
	}, "readWriteAnyDatabase"]
});
```

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
然后我们切换到 `test` 数据库，创建一个 `test` 用户，我们所有的学习都基于这个 `test` 数据库来进行，与上面类似，执行下面两个指令：
=======
然后我们切换到`test`数据库，创建一个`test`用户，我们所有的学习都基于这个`test`数据库来进行，与上面类似，执行下面两个指令：
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

```
# 1. 切换到test，说明一下，use指令切换数据库时，如果数据库不存在，会自动创建的

use test

# 2. 创建一个对test数据库具有读写权限的用户test

db.createUser({
	user: "test",
	pwd: passwordPrompt(), // or cleartext password
	roles: [{
		role: "readWrite",
		db: "test"
	}]
})
执行完这条语句后，会提示我们输入该用户的密码，输入完成，用户就创建成功了。
```

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
关于 `MongoDB` 其他知识，参考 [MongoDB 官网](https://docs.mongodb.com/manual/)

# 创建 SpringBoot 项目，整合 `MongoDB` 和 `Docker`

我们通过 `SpringBoot` 项目来整合 `MongoDB` 和 `Docker`，然后通过 `Swagger` 来测试

##### 1. `MongoDB` 和 `Swagger` 依赖配置
=======
关于`MongoDB`其他知识，参考 [MongoDB官网](https://docs.mongodb.com/manual/)

# 创建SpringBoot项目，整合`MongoDB` 和 `Docker`

我们通过`SpringBoot`项目来整合`MongoDB`和`Docker`,然后通过`Swagger` 来测试

##### 1. `MongoDB`和`Swagger`依赖配置
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

```
<!--   mongodb     -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-mongodb</artifactId>
        </dependency>
        <!--   web     -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--   lombok     -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <!-- swagger -->
        <dependency>
            <groupId>com.spring4all</groupId>
            <artifactId>swagger-spring-boot-starter</artifactId>
            <version>1.7.0.RELEASE</version>
        </dependency>
        <!--   启动类加上@EnableSwagger2Doc注解后,如果不加validation这个依赖,启动会失败,目前原因不明     -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>
```

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
##### 2. `Docker` 插件配置
=======
##### 2. `Docker`插件配置
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

```
<properties>
        <java.version>1.8</java.version>
	<!-- dcoker 插件版本 -->
        <docker.maven.plugin.version>1.2.2</docker.maven.plugin.version>
        <docker.image.prefix>springboot</docker.image.prefix>
    </properties>
```

```
<!--     docker 配置       -->
        <plugin>
            <groupId>com.spotify</groupId>
            <artifactId>docker-maven-plugin</artifactId>
            <version>${docker.maven.plugin.version}</version>
            <configuration>
                <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
		<!--  指定Dockfile文件所在位置  -->
                <dockerDirectory>src/main/docker</dockerDirectory>
                <resources>
                    <resource>
                        <targetPath>/</targetPath>
                        <directory>${project.build.directory}</directory>
                        <include>${project.build.finalName}.jar</include>
                    </resource>
                </resources>
            </configuration>
        </plugin>
```

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
##### 3. `MongoDB` 连接配置
=======
##### 3. `MongoDB`连接配置
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

```
spring:
  data:
    mongodb:
      database: test
      host: 127.0.0.1
      port: 27017
      username: test
      password: test
```

##### 4. 代码

实体类

```
@Data
public class Book {
    private Integer id;
    private String name;
    private String author;
    private String description;
}
```

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
操作 `MongoDB` 数据库主要通过注入 `MongoTemplate` 来实现
=======
操作`MongoDB`数据库主要通过注入`MongoTemplate`来实现
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

```
@Service
public class BookService {

    @Autowired
    private MongoTemplate mongoTemplate;

    /**
     *  保存
     *
     * @param book
     */
    public void save(Book book) {
        mongoTemplate.save(book);
    }


    /**
     *  根据ID查询
     *
     * @param id
     * @return
     */
    public Book findById(Integer id) {
       return mongoTemplate.findOne(Query.query(Criteria.where("id").is(id)), Book.class);
    }

    /**
     *  根据名字查询
     *
     * @param name
     * @return
     */
    public Book findByName(String name) {
       return mongoTemplate.findOne(Query.query(Criteria.where("name").is(name)), Book.class);
    }

    /**
     *  查询所有
     *
     * @return
     */
    public List<Book> findAll() {
        return mongoTemplate.findAll(Book.class);
    }

    /**
     *  更新
     *
     * @param book
     */
    public void update(Book book) {
        Query query = Query.query(Criteria.where("id").is(book.getId()));
        Update update = Update.update("name", book.getName()).set("author", book.getAuthor())
                .set("description", book.getDescription());
        mongoTemplate.updateFirst(query, update, Book.class);
    }


    /**
     *  删除
     *
     * @param id
     */
    public void delete(Integer id) {
        mongoTemplate.remove(Query.query(Criteria.where("id").is(id)), Book.class);
    }


}
```

控制层

```
@RestController
@RequestMapping("/book")
@Api(value = "书籍管理", tags = "book")
public class BookController {

    @Autowired
    private BookService bookService;

    @PostMapping("/save")
    @ApiOperation(value = "保存")
    public void save(@RequestBody Book book) {
        this.bookService.save(book);
    }

    @GetMapping("/getById/{id}")
    @ApiOperation(value = "根据ID查询")
    public Book getById(@PathVariable Integer id) {
        return bookService.findById(id);
    }

    @GetMapping("/getByName/{name}")
    @ApiOperation(value = "根据名称查询")
    public Book getByName(@PathVariable String name) {
        return bookService.findByName(name);
    }


    @GetMapping("/getAll")
    @ApiOperation(value = "查询所有")
    public List<Book> getAll() {
        return bookService.findAll();
    }


    @PutMapping("/update")
    @ApiOperation(value = "更新")
    public void update(@RequestBody Book book) {
        bookService.update(book);
    }

    @DeleteMapping("/delete{id}")
    @ApiOperation(value = "删除")
    public void delete(@PathVariable Integer id) {
        bookService.delete(id);
    }
}
```

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
###### 5. 编写 `Dockfile` 文件

打包之前需要先编写一个 `Dcokerfile` 文件，这个文件我放在 `/src/main/docker/目录下`，`Dockerfile` 的具体配置，可以看看这个 [Docker Dockerfile](https://www.runoob.com/docker/docker-dockerfile.html)
=======
###### 5. 编写`Dockfile`文件

打包之前需要先编写一个`Dcokerfile`文件，这个文件我放在`/src/main/docker/目录下`，`Dockerfile`的具体配置，可以看看这个 [Docker Dockerfile](https://www.runoob.com/docker/docker-dockerfile.html)
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

```
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ADD springboot-mongodb-docker-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
##### 6. 将项目打包为 `Docker` 镜像

进入项目所在目录，执行 `mvn package docker:build` 命令，如果没有报错，就说明打包成功，此时执行 `docker images` 指令查看镜像，第一个就是我们打包的镜像
=======
##### 6. 将项目打包为`Docker`镜像

进入项目所在目录，执行`mvn package docker:build`命令，如果没有报错，就说明打包成功，此时执行`docker images`指令查看镜像，第一个就是我们打包的镜像
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

![spingbootdockerimage.png](https://b3logfile.com/file/2020/09/spingbootdockerimage-780f6fe0.png)

##### 7. 启动镜像

指令：`docker run -d --net=host -p 8080:8080 --name springboot-mongodb-docker springboot/springboot-mongodb-docker:latest`

参数说明：

- -d : 后台运行
- --net=host: 使用 host 模式启动容器，此时容器和宿主机共用一个 Network Namespace，这样我们的容器才可以访问其他运行着的软件，比如 `MongoDB`
- -p : 指定端口号
- --name: 指定我们容器的名字

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
如果我们想查看项目的日志，可以通过指令 `docker logs springboot-mongodb-docker > logs.txt` 来将日志写到 `logs.txt` 文件中

##### 8. 通过 `Swagger` 测试

在浏览器输入 [http://localhost:8080/swagger-ui.html#/](http://localhost:8080/swagger-ui.html#/)
=======
如果我们想查看项目的日志，可以通过指令`docker logs springboot-mongodb-docker > logs.txt`来将日志写到`logs.txt`文件中

##### 8. 通过`Swagger`测试

在浏览器输入[http://localhost:8080/swagger-ui.html#/](http://localhost:8080/swagger-ui.html#/)
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

测试保存接口

![booksave2.png](https://b3logfile.com/file/2020/09/booksave2-15dddb5d.png)

测试查询接口

![bookfind.png](https://b3logfile.com/file/2020/09/bookfind-9f3c7dd0.png)

进入数据库查看

![mogofind.png](https://b3logfile.com/file/2020/09/mogofind-61958c1b.png)

至此，我们就成功了 😄

# 总结

<<<<<<< HEAD:pl/java/spring-boot/SpringBoot整合Docker和MongoDB 笔记_20201010174802-1p38s85.sy.md
通过 `Docker` 安装软件，是非常便利的，只需要学会 `docker pull ` 和 `docker run` 两个指令就可以了。同时，`docker` 和 `SpringBoot` 的整合，使我们部署维护项目也变得很简单。
=======
通过`Docker`安装软件，是非常便利的，只需要学会`docker pull ` 和 `docker run`两个指令就可以了。同时，`docker`和 `SpringBoot`的整合，使我们部署维护项目也变得很简单。
>>>>>>> ba9f78b2d7c3075d2c8bad751a27c9701c42d547:pl/java/spring-boot/SpringBoot整合Docker和MongoDB笔记_20201010174802-1p38s85.sy.md

完整代码 [springboot-mongodb-docker](https://github.com/marshalby2/springboot-mongodb-docker)
