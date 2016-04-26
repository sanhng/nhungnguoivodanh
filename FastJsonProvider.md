FastJson 提供了JAX-RS Provider的实现 [FastJsonProvider] (https://github.com/alibaba/fastjson/blob/master/src/main/java/com/alibaba/fastjson/support/jaxrs/FastJsonProvider.java) 

可用于在构建Restful服务时使用FastJson进行数据的Serialize and Deserialize

以[Apache CXF Restful](http://cxf.apache.org/docs/jax-rs.html)为例的Spring XML配置如下

```xml
<bean id="fastJsonProvider" class="com.alibaba.fastjson.support.jaxrs.FastJsonProvider">
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

<jaxrs:server id="restfulServer" address="/">
	<jaxrs:inInterceptors>
		<bean class="org.apache.cxf.interceptor.LoggingInInterceptor" />
	</jaxrs:inInterceptors>
	<jaxrs:outInterceptors>
		<bean class="org.apache.cxf.interceptor.LoggingOutInterceptor" />
	</jaxrs:outInterceptors>
	<jaxrs:serviceBeans>
		<ref bean="Your service" />
	</jaxrs:serviceBeans>
	<jaxrs:providers>
		<ref bean="fastJsonProvider" />	<!-- FastJsonProvider -->
	</jaxrs:providers>
	<jaxrs:extensionMappings>
		<entry key="json" value="application/json" />
	</jaxrs:extensionMappings>
	<jaxrs:languageMappings>
		<entry key="en" value="en-gb" />
	</jaxrs:languageMappings>
</jaxrs:server>
```