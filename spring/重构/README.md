### 解耦

#### 调度

解耦调度与公司内部调度平台，使用spring自带调度，灵活配置调度的开启和关闭

##### 原理

开启Spring调度是在启动类添加@EnableScheduling

```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Import({SchedulingConfiguration.class})
@Documented
public @interface EnableScheduling {
}
```

通过@Import注解来注入SchedulingConfiguration的bean对象

类似的我们利用spring的动态配置@ConditionalOnExpression来动态注入或者不注入对象来实现

```java
@Configuration
@ConditionalOnExpression(value = "${spring.scheduling.enabled}")
@Import(SchedulingConfiguration.class)
public class ControlSchedulingConfig {
}
```

spring.scheduling.enabled写在配置文件，true开启，false关闭

同时使用简单的redis分布式锁来防止多台机器同时执行调度

#### 中间件解耦

中间件解耦，例如：mq使用jmq、kafka等来灵活配置

##### 原理

利用@Conditional注解，以及springboot衍生的注解和AllNestedConditions、AnyNestedCondition这2个类来进行条件注入来进行条件注入

```java
@ConditionalOnProperty：如果有指定的配置，条件生效；
@ConditionalOnBean：如果有指定的Bean，条件生效；
@ConditionalOnMissingBean：如果没有指定的Bean，条件生效；
@ConditionalOnMissingClass：如果没有指定的Class，条件生效；
@ConditionalOnWebApplication：在Web环境中条件生效；
@ConditionalOnExpression：根据表达式判断条件是否生效，true才生效
```

根据SpringBoot启动类注解源码查看

@SpringBootApplication->@EnableAutoConfiguration->AutoConfigurationImportSelector

找到jar包：autoconfigure下，通过spring.factories文件来配置加载不同三方中间键

```java
@ConditionalOnClass：只有在classpath能找到class的时候才加载
```

MQ注意：

1、根据配置文件灵活加载product

2、根据配置文件加载对应的consumer,监听消息，给到对应的bean处理消息

