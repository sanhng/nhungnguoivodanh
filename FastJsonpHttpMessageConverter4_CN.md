FastJson 提供了Spring MVC HttpMessageConverter的实现，将POJO输出为JSONP，支持跨域数据访问。

* [FastJsonpHttpMessageConverter4](https://github.com/alibaba/fastjson/blob/master/src/main/java/com/alibaba/fastjson/support/spring/FastJsonpHttpMessageConverter4.java) for Spring MVC 4.2+

# 需求

客户端异步请求后端服务接口，前后端不在同一个域名下，需要跨域数据访问。

# 客户端使用方法

```javascript
curl http://server:port/user/find/1?callback=javaScriptFunction
// javaScriptFunction：JavaScript代码中的回调函数名
// callback：Java代码中约定的请求参数
```

# 后端配置代码

## 使用`xml`配置

```xml
<mvc:annotation-driven>
    <mvc:message-converters>
        <bean
            class="com.alibaba.fastjson.support.spring.FastJsonpHttpMessageConverter4">
            <property name="supportedMediaTypes">
                <list>
                    <value>application/json;charset=UTF-8</value>
                </list>
            </property>
        </bean>
    </mvc:message-converters>
</mvc:annotation-driven>

<mvc:default-servlet-handler />

<bean id="fastJsonpResponseBodyAdvice" class="com.alibaba.fastjson.support.spring.FastJsonpResponseBodyAdvice">
    <constructor-arg>
        <list>
            <value>callback</value>
            <value>jsonp</value>
        </list>
    </constructor-arg>
</bean>

```

## 使用`Java`代码配置

```java
@EnableWebMvc
@Configuration
public class Config extends WebMvcConfigurerAdapter {
    @Bean
    public FastJsonpResponseBodyAdvice fastJsonpResponseBodyAdvice() {
        return new FastJsonpResponseBodyAdvice("callback", "jsonp");
    }

    @Override
    public void extendMessageConverters(List<HttpMessageConverter<?>> converters) {
        converters.add(0, new FastJsonpHttpMessageConverter4());
        super.extendMessageConverters(converters);
    }
}
```

spring boot项目中可以不继承`WebMvcConfigurerAdapter `

```java
@Configuration
public class Config{
    @Bean
    public FastJsonpResponseBodyAdvice fastJsonpResponseBodyAdvice() {
        return new FastJsonpResponseBodyAdvice("callback", "jsonp");
    }

    @Bean
    public FastJsonpHttpMessageConverter4 fastJsonpHttpMessageConverter4() {
        return new FastJsonpHttpMessageConverter4();
    }
}
```
