- [脚本](#脚本)
- [配置](#配置)
  - [cookie自动映射变量](#cookie自动映射变量)

# 脚本

```groovy
import org.apache.jmeter.protocol.http.control.HeaderManager;
import org.apache.jmeter.protocol.http.control.Header;
import org.apache.commons.codec.digest.DigestUtils;

// 设置和获取props属性，props可以跨线程组使用
// vars.get vars.put类似，但是仅限于线程组内
props.put("salt", "123");
props.get("salt");
vars.put("salt", "123");
vars.get("salt");

// 获取当前时间戳
System.currentTimeMillis();

// 获取请求路径
sampler.getPath().toString();
// 获取请求全部请求路径
sampler.getUrl()
// 获取请求体内容
sampler.getArguments().getArgument(0).getValue();
// 获取查询参数
sampler.getQueryString()

// md5加密示例(注意，一般此类加密，请求体内容需要写成字符串形式，不要写成json格式，否则某些换行和空格无法处理)
// 比如在body data里面输入 {"account": "ystest_auto_user1", "accountType": "inter", "email": "test@test.cn"}
String x_sn = "/api/user" + reqBody + x_t + x_st;
x_sn = DigestUtils.md5Hex(x_sn);
    
// 请求头处理
HeaderManager headers = sampler.getHeaderManager();
if (headers == null) {
	  headers = new HeaderManager();
}
if (headers.size() > 0) {
	  headers.clear();
}
headers.add(new Header("x-t", x_t));
headers.add(new Header("x-st", x_st));
headers.add(new Header("x-sn", x_sn));
headers.add(new Header("Content-Type", "application/json"));
sampler.setHeaderManager(headers);
```

# 配置

## cookie自动映射变量

1. 修改`bin/jmeter.properties`配置文件

```ini
# CookieManager behaviour - should Cookies be stored as variables?
# Default is false
; 把下面的配置改为true，就可以自动把cookie映射为变量
CookieManager.save.cookies=true

; 下面是变量的前缀，默认是COOKIE_
; 比如某个请求的响应头: Set-Cookie: VS=86e11953-8a32-4c50-9b95-5f6fbd4a06c8，那么会产生一个COOKIE_VS的变量
; 可以有多个，在脚本里面就可以通过${COOKIE_VS}获取这个变量的值
# CookieManager behaviour - prefix to add to cookie name before storing it as a variable
# Default is COOKIE_; to remove the prefix, define it as one or more spaces
#CookieManager.name.prefix=
```