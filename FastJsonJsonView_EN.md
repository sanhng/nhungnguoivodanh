**Spring has not recommend, see [FastJsonHttpMessageConverter](https://github.com/alibaba/fastjson/wiki/FastJsonHttpMessageConverter_EN).**

[FastJsonJsonView](https://github.com/alibaba/fastjson/blob/master/src/main/java/com/alibaba/fastjson/support/spring/FastJsonJsonView.java) is a Spring MVC AbstractView implementor.

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
            <ref bean="Your serializer filter"/>	
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

_FastJsonJsonView Configuration_
```xml
<bean id="fastJsonJsonView" class="com.alibaba.fastjson.support.spring.FastJsonJsonView">
    <property name="fastJsonConfig" ref="fastJsonConfig"/>
</bean>

<bean
	class="org.springframework.web.servlet.view.ContentNegotiatingViewResolver">
	<property name="order" value="1" />
	<property name="contentNegotiationManager">
		<bean class="org.springframework.web.accept.ContentNegotiationManager">
			<constructor-arg>
				<bean class="org.springframework.web.accept.PathExtensionContentNegotiationStrategy">
					<constructor-arg>
						<map>
							<entry key="json" value="application/json" />
						</map>
					</constructor-arg>
				</bean>
			</constructor-arg>
		</bean>
	</property>
	<property name="defaultViews">
		<list>
			<ref bean="fastJsonJsonView"/>
		</list>
	</property>
</bean>
```