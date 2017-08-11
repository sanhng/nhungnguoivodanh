## Integrate Fastjson in JAX-RS

Fastjson has implemented JAX-RS, You can use FastJson in Restfull Service for data Serialize and Deserialize.

### Use Fastjson in Apache CXF

With Apache CXF Restful and Spring Framework, for example

```xml

<bean id="fastJsonConfig" class="com.alibaba.fastjson.support.config.FastJsonConfig">
	<!-- ... -->
</bean>

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
> REF: [Apache CXF Restful official document](http://cxf.apache.org/docs/jax-rs.html)

### Use Fastjson in Jersey

User register codes, since version 1.2.37 (recommend)

```java
@Provider
static class FastJsonResolver implements ContextResolver<FastJsonConfig> {

    public FastJsonConfig getContext(Class<?> type) {

        FastJsonConfig fastJsonConfig = new FastJsonConfig();

        /* ... */

        return fastJsonConfig;
    }
}

public class RestApplication extends ResourceConfig { 
 
    public RestApplication() {     

     packages("com.xxx.xxx");  

     /* ... */

     register(FastJsonResolver.class);     

     register(FastJsonFeature.class);  
    }  
}  
```

_Note: Fastjson also provided auto register when you don't have to user register in Jersey, default is enabled, if you don't want this, you can_

```java 
FastJsonAutoDiscoverable.autoDiscover = false;
```

> REF: [Jersey deployment official document](https://jersey.github.io/documentation/latest/deployment.html)
