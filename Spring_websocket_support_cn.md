在fastjson-1.2.16版本开始，新增加spring websocket支持，支持的实现如下：
```java
com.alibaba.fastjson.support.spring.FastjsonSockJsMessageCodec
```
初始支持，遇到问题请大家反馈


```java
@Component
@EnableWebSocket
public class WebSocketConfig extends WebMvcConfigurerAdapter implements WebSocketConfigurer {

	@Resource
	WebSocketHandler handler;

	public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
		registry.addHandler(handler, "/sockjs").withSockJS().setMessageCodec(new FastjsonSockJsMessageCodec());
	}

}
```