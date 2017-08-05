### 在 Spring MVC 中集成 Fastjson
如果你使用 Spring MVC 并且对 Web 应用性能有较高的要求，那么你可以使用 ```FastJsonHttpMessageConverter``` 来替换默认的 ```HttpMessageConverter```  提高 `@RestController @ResponseBody @RequestBody` 注解的 JSON序列化速度，配置非常简单，下面是配置方式。
#### XML式
如果是使用编程的方式配置 Spring MVC 的话，只需在 Spring MVC 的 XML 配置文件中加入下面配置即可。
```xml
<mvc:annotation-driven>
    <mvc:message-converters>
        <bean class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter"/>      
    </mvc:message-converters>
</mvc:annotation-driven>

```
通常默认配置已经可以满足大部分使用场景，如果你想对它进行自定义配置的话，你可以添加 ```FastJsonConfig``` Bean。
```xml
<mvc:annotation-driven>
    <mvc:message-converters>
        <bean class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter">
            <property name="fastJsonConfig" ref="fastJsonConfig"/>
        </bean>
    </mvc:message-converters>
</mvc:annotation-driven>

<bean id="fastJsonConfig" class="com.alibaba.fastjson.support.config.FastJsonConfig">
    <!--   自定义配置...   -->
</bean>
```
#### 编程式
如果是使用编程的方式（通常是基于 Spring Boot 项目）配置 Spring MVC 的话只需继承 ```WebMvcConfigurerAdapter``` 覆写 ```configureMessageConverters``` 方法即可，就像下面这样。
```java
@Configuration
public class WebMvcConfigurer extends WebMvcConfigurerAdapter {
    @Override
    public void configureMessageConverters(List<HttpMessageConverter<?>> converters) {
        FastJsonHttpMessageConverter converter = new FastJsonHttpMessageConverter();
        //自定义配置...
        //FastJsonConfig config = new FastJsonConfig();
        //config.set ...
        //converter.setFastJsonConfig(config);
        converters.add(converter);
    }
}
```
注：如果你使用的是 Fastjson 版本小于```1.2.36```的话(强烈建议使用最新版本)，在Spring MVC 4.X 时需使用 ```FastJsonHttpMessageConverter4```