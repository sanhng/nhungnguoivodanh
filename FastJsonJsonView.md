**此方式已不被Spring推荐 建议采用[FastJsonHttpMessageConverter](https://github.com/alibaba/fastjson/wiki/FastJsonHttpMessageConverter)**

FastJson 提供了Spring MVC AbstractView的实现 [FastJsonJsonView](https://github.com/alibaba/fastjson/blob/master/src/main/java/com/alibaba/fastjson/support/spring/FastJsonJsonView.java)

可用于在Spring Controller中使用FastJson进行数据的Serialize and Deserializ

Spring XML配置如下

```xml

	<bean id="fastJsonJsonView" class="com.alibaba.fastjson.support.spring.FastJsonJsonView">
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
		...
	</bean>

	<bean
		class="org.springframework.web.servlet.view.ContentNegotiatingViewResolver">
		<property name="order" value="1" />
		<property name="contentNegotiationManager">
			<bean class="org.springframework.web.accept.ContentNegotiationManager">
				<constructor-arg>
					<bean
						class="org.springframework.web.accept.PathExtensionContentNegotiationStrategy">
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