# 安全公告20200601
近日，阿里云应急响应中心监测到fastjson爆发新的反序列化远程代码执行漏洞，黑客利用漏洞，可绕过autoType限制，直接远程执行任意命令攻击服务器，风险极大。

# 漏洞描述
fastjson采用黑白名单的方法来防御反序列化漏洞，导致当黑客不断发掘新的反序列化Gadgets类时，在autoType关闭的情况下仍然可能可以绕过黑白名单防御机制，造成远程命令执行漏洞。经研究，该漏洞利用门槛较低，可绕过autoType限制，风险影响较大。阿里云应急响应中心提醒fastjson用户尽快采取安全措施阻止漏洞攻击。

# 影响版本
* fastjson <=1.2.68
* fastjson sec版本 <= sec9
* android版本不受此漏洞影响

# 升级方案
升级到最新版本1.2.69或者更新的1.2.70版本。
* 1.2.69 https://github.com/alibaba/fastjson/releases/tag/1.2.69
* 1.2.79 https://github.com/alibaba/fastjson/releases/tag/1.2.70

如果遇到兼容问题，原地升级sec10版本。
* 1.1.15~1.1.31 -> [1.1.31.sec10](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.1.31.sec10)
* 1.1.32~1.1.33 -> [1.1.33.sec10](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.1.33.sec10)
* 1.1.34        -> [1.1.34.sec10](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.1.34.sec10)
* 1.1.35~1.1.46 -> [1.1.46.sec10](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.1.46.sec10)
* 1.2.0~1.2.2   -> [1.2.2.sec10](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.2.sec10) 因为1.2.3之后的版本Map是没有排序输出的，如果不关注这个兼容问题，升级到1.2.70
* 1.2.3~1.2.7   -> [1.2.7.sec10](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.7.sec10) 因为1.2.7使用最多特别提供，也可以直接使用1.2.8.sec10
* 1.2.8 -> [1.2.8.sec10](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.8.sec10)
* 1.2.9~1.2.29 -> [1.2.29.sec10](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.29.sec10)
* 1.2.30~1.2.48 -> [1.2.48.sec10](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.48.sec10)
* 1.2.49~1.2.68 -> [1.2.69](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.69)或[1.2.70](https://repo1.maven.org/maven2/com/alibaba/fastjson/1.2.70)
中间有很多sec10小版本，建议直接升级到1.2.69或1.2.70，如果遇到兼容再考虑sec10版本

如果还遇到其他兼容问题，这里有更多的sec10版本 https://repo1.maven.org/maven2/com/alibaba/fastjson/

# fastjson加固
fastjson在1.2.68及之后的版本中引入了safeMode，配置safeMode后，无论白名单和黑名单，都不支持autoType，可一定程度上缓解反序列化Gadgets类变种攻击（关闭autoType注意评估对业务的影响）
* 开启方法参考： https://github.com/alibaba/fastjson/wiki/fastjson_safemode

