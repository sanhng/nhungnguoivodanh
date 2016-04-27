FastJson 提供了JAX-RS Provider的实现 [FastJsonProvider] (https://github.com/alibaba/fastjson/blob/master/src/main/java/com/alibaba/fastjson/support/jaxrs/FastJsonProvider.java) 

可用于在构建Restful服务时使用FastJson进行数据的Serialize and Deserialize

以[Apache CXF Restful](http://cxf.apache.org/docs/jax-rs.html)为例的Spring XML配置如下

FastJsonConfig配置
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

FastJsonProvider配置
```xml
<bean id="fastJsonProvider" class="com.alibaba.fastjson.support.jaxrs.FastJsonProvider">
	<property name="fastJsonConfig" ref="fastJsonConfig"/>
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