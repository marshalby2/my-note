# BUG1
{: id="20210104221219-484eure"}

今天升级了 SpringBoot 和 SpringCloud 的版本，就遇到了这个问题， 无法解决
{: id="20210104221225-cfvu6f9"}

```java
java.lang.IllegalArgumentException: Unable to instantiate factory class [org.springframework.boot.context.config.ConfigDataEnvironmentPostProcessor] for factory type [org.springframework.boot.env.EnvironmentPostProcessor]
	at org.springframework.core.io.support.SpringFactoriesLoader.instantiateFactory(SpringFactoriesLoader.java:168)
	at org.springframework.core.io.support.SpringFactoriesLoader.loadFactories(SpringFactoriesLoader.java:104)
	at org.springframework.boot.context.config.ConfigFileApplicationListener.loadPostProcessors(ConfigFileApplicationListener.java:205)
	at org.springframework.boot.context.config.ConfigFileApplicationListener.onApplicationEnvironmentPreparedEvent(ConfigFileApplicationListener.java:196)
	at org.springframework.boot.context.config.ConfigFileApplicationListener.onApplicationEvent(ConfigFileApplicationListener.java:188)
	at org.springframework.context.event.SimpleApplicationEventMulticaster.doInvokeListener(SimpleApplicationEventMulticaster.java:172)
	at org.springframework.context.event.SimpleApplicationEventMulticaster.invokeListener(SimpleApplicationEventMulticaster.java:165)
	at org.springframework.context.event.SimpleApplicationEventMulticaster.multicastEvent(SimpleApplicationEventMulticaster.java:139)
	at org.springframework.context.event.SimpleApplicationEventMulticaster.multicastEvent(SimpleApplicationEventMulticaster.java:127)
	at org.springframework.boot.context.event.EventPublishingRunListener.environmentPrepared(EventPublishingRunListener.java:80)
	at org.springframework.boot.SpringApplicationRunListeners.environmentPrepared(SpringApplicationRunListeners.java:53)
	at org.springframework.boot.SpringApplication.prepareEnvironment(SpringApplication.java:345)
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:308)
	at org.springframework.boot.builder.SpringApplicationBuilder.run(SpringApplicationBuilder.java:140)
	at org.springframework.cloud.bootstrap.BootstrapApplicationListener.bootstrapServiceContext(BootstrapApplicationListener.java:212)
	at org.springframework.cloud.bootstrap.BootstrapApplicationListener.onApplicationEvent(BootstrapApplicationListener.java:117)
	at org.springframework.cloud.bootstrap.BootstrapApplicationListener.onApplicationEvent(BootstrapApplicationListener.java:74)
	at org.springframework.context.event.SimpleApplicationEventMulticaster.doInvokeListener(SimpleApplicationEventMulticaster.java:172)
	at org.springframework.context.event.SimpleApplicationEventMulticaster.invokeListener(SimpleApplicationEventMulticaster.java:165)
	at org.springframework.context.event.SimpleApplicationEventMulticaster.multicastEvent(SimpleApplicationEventMulticaster.java:139)
	at org.springframework.context.event.SimpleApplicationEventMulticaster.multicastEvent(SimpleApplicationEventMulticaster.java:127)
	at org.springframework.boot.context.event.EventPublishingRunListener.environmentPrepared(EventPublishingRunListener.java:80)
	at org.springframework.boot.SpringApplicationRunListeners.environmentPrepared(SpringApplicationRunListeners.java:53)
	at org.springframework.boot.SpringApplication.prepareEnvironment(SpringApplication.java:345)
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:308)
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1237)
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1226)
	at com.my.EurekaServerApplication.main(EurekaServerApplication.java:12)
Caused by: java.lang.NoSuchMethodException: org.springframework.boot.context.config.ConfigDataEnvironmentPostProcessor.<init>()
	at java.base/java.lang.Class.getConstructor0(Class.java:3508)
	at java.base/java.lang.Class.getDeclaredConstructor(Class.java:2711)
	at org.springframework.util.ReflectionUtils.accessibleConstructor(ReflectionUtils.java:185)
	at org.springframework.core.io.support.SpringFactoriesLoader.instantiateFactory(SpringFactoriesLoader.java:164)
	... 27 common frames omitted
Disconnected from the target VM, address: '127.0.0.1:60070', transport: 'socket'

```
{: id="20210104221201-6jq8kak"}
