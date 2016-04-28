This is a Spring MVC HttpMessageConverter implementor.

* [FastJsonHttpMessageConverter](https://github.com/alibaba/fastjson/blob/master/src/main/java/com/alibaba/fastjson/support/spring/FastJsonHttpMessageConverter.java) for Spring MVC Below 4.2
* [FastJsonHttpMessageConverter4](https://github.com/alibaba/fastjson/blob/master/src/main/java/com/alibaba/fastjson/support/spring/FastJsonHttpMessageConverter4.java) for Spring MVC 4.2+

It can be use FastJson in Spring MVC Controller for data Serialize and Deserialize.

_FastJsonConfig Configuration_
```xml
<bean id="fastJsonConfig" class="com.alibaba.fastjson.support.config.FastJsonConfig">
	<!-- Default charset -->
	<property name="charset" value="UTF-8" />
	<!-- Default dateFormat -->
	<property name="dateFormat" value="yyyy-MM-dd HH:mm:ss" />
	<!-- Feature -->
	<property name="features">
		<list>
			<value>Your feature</value>
		</list>
	</property>
	<!-- SerializerFeature -->
	<property name="serializerFeatures">
		<list>
			<value>Your serializer feature</value>
		</list>
	</property>
	<!-- Global SerializeFilter -->
	<property name="serializeFilters">
		<list>
			<value>Your serializer filter</value>
		</list>
	</property>
	<!-- Class Level SerializeFilter -->
	<property name="classSerializeFilters">
		<map>
			<entry key="Your filter class" value-ref="Your serializer filter"/>
		</map>
	</property>
</bean>
```

_HttpMessageConverter Configuration_
```xml
<mvc:annotation-driven>
	<mvc:message-converters>
		<bean class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter">
			<!-- MediaTypes -->
			<property name="supportedMediaTypes">
				<list>
					<value>application/json</value>
				</list>
			</property>
			<!-- FastJsonConfig -->
			<property name="fastJsonConfig" ref="fastJsonConfig" />
		</bean>
	</mvc:message-converters>
</mvc:annotation-driven>

<mvc:default-servlet-handler />
```