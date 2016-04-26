FastJson 提供了Spring MVC HttpMessageConverter的实现

* [FastJsonHttpMessageConverter](https://github.com/alibaba/fastjson/blob/master/src/main/java/com/alibaba/fastjson/support/spring/FastJsonHttpMessageConverter.java) for Spring MVC Below 4.2
* [FastJsonHttpMessageConverter4](https://github.com/alibaba/fastjson/blob/master/src/main/java/com/alibaba/fastjson/support/spring/FastJsonHttpMessageConverter4.java) for Spring MVC 4.2+

可用于在Spring Controller中使用FastJson进行数据的Serialize and Deserialize

Spring XML配置如下

```xml
<mvc:annotation-driven>
	<mvc:message-converters>
		<bean class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter">
			<!-- SupportedMediaTypes[] -->
			<property name="supportedMediaTypes">
				<list>
					<value>application/json</value>
				</list>
			</property>
			<!-- SerializerFeature[] -->
			<property name="features">
				<list>
					<value>Your feature</value>
				</list>
			</property>
			<!-- SerializeFilter[] -->
			<property name="filters">
				<list>
					<ref bean="Your filter" />
				</list>
			</property>
		</bean>
	</mvc:message-converters>
</mvc:annotation-driven>

<mvc:default-servlet-handler />
```