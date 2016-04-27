**此方式已不被Spring推荐 建议采用[FastJsonHttpMessageConverter](https://github.com/alibaba/fastjson/wiki/FastJsonHttpMessageConverter)**

FastJson 提供了Spring MVC AbstractView的实现 [FastJsonJsonView](https://github.com/alibaba/fastjson/blob/master/src/main/java/com/alibaba/fastjson/support/spring/FastJsonJsonView.java)

可用于在Spring Controller中使用FastJson进行数据的Serialize and Deserializ

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

FastJsonJsonView配置
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