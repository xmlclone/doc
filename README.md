- [说明](#说明)
  - [need known](#need-known)
- [测试基础](#测试基础)
  - [测试分类](#测试分类)
  - [标准建立](#标准建立)
    - [用例级别](#用例级别)
    - [缺陷级别](#缺陷级别)
    - [通过标准](#通过标准)
    - [提测标准(准入标准)](#提测标准准入标准)
    - [打回标准](#打回标准)
    - [测试过程限制](#测试过程限制)
  - [测试计划](#测试计划)
  - [风险识别](#风险识别)
  - [效率评估](#效率评估)
- [测试类型](#测试类型)
  - [性能测试](#性能测试)
  - [自动化](#自动化)
  - [专项](#专项)
- [技术\&工具](#技术工具)
  - [Python](#python)
    - [图形处理](#图形处理)
  - [Groovy](#groovy)
  - [Javascript](#javascript)
  - [Jmeter](#jmeter)
    - [常用代码合集](#常用代码合集)
  - [Selenium](#selenium)
  - [Flask](#flask)
- [系统知识](#系统知识)
- [附件\&模板](#附件模板)
  - [附件1：常用链接](#附件1常用链接)
  - [附件2：常见问题](#附件2常见问题)
    - [安装jdk后，没有jre目录](#安装jdk后没有jre目录)

# 说明
1. 每个章节前均会简要列举重点事项，不需要太过详细，也不需要很强的逻辑说明，可以理解为一个摘要，如果能根据这个摘要联想后续的详细内容，建议后续内容也没必要详细看了。

## need known

1. 4层负载(3层呢？ nginx lsv呢？)
2. socketio负载

# 测试基础

## 测试分类

自研、验收、合作
黑盒、白盒、灰盒
功能、性能、稳定性、安全、兼容

## 标准建立

### 用例级别

每个公司要求可能不一致，但基本符合以下原则：

P1：保证基本功能、基本特性、实际使用频率比较高的用例,该级别的测试用例在每一轮版本测试中都必须执行。指最重要最基础的主要功能，含需求的核心流程、唯一路径、必要要求等。如果执行不通过，会阻塞后续相关测试工作的用例。(每个版本、每轮测试必须测试，包括冒烟、首轮、次轮、回归、上线验证等流程必须执行，也就是不管这个功能是哪个版本提测的，只要是测这个系统，就必须每轮进行测试)

P2：主要包括一些功能交互相关、个种应用场景、使用频率较高的正常功能测试;在非回归的系统测试版本中基本上都需要进行验证，以保证系统所有的重要功能都能够正常实现。(版本首轮、次轮都应该执行；冒烟、回归、上线可选，非当前版本提测的功能可以不执行，注意不是当前版本提测的内容，但是在首轮和次轮也应该要覆盖测试)

P3：实际使用频率不高、对系统业务功能影响不大的模块或功能、界面检查、异常功能等测试用例。(一般只需要在实现的版本测试即可)

### 缺陷级别

缺陷等级：致命P0、严重P1、一般P2、轻微P3
 
一、致命P0：
1、稳定复现的闪退、卡死
2、资金漏洞（比如：支付相关问题，对公司营收造成影响的）
4、服务宕机
5、系统崩溃、挂机、死机
6、主要功能完全丧失
7、主流程阻塞性问题，且不可通过其他操作绕过，用户无法继续使用产品
8、用户数据受到破坏，且不可恢复
9、常规操作造成程序非法退出、死循环、通讯中断或者异常、内存溢出
10、数据库异常，数据无法正常存储或查询
 
降级标准：
1、线上已存在但无人反馈可以降级
2、影响用户数量较少可以降级
3、非主流机型，可以降级
 
二、严重P1：
1、阻塞性问题，但可通过其他操作绕过，继续使用
2、主要功能部分丧失、数据不能保存，但可通过其他方法实现
3、系统的次要功能完全丧失
4、系统所提供的功能或者服务受到严重影响
5、错误的波及面广，影响到其他重要功能正常使用
6、客户端某些操作导致服务端不能继续正常工作
7、密码明文展示
 
降级标准：
1、非主要路径可以降级
2、线上已存在但无人反馈可以降级
 
三、一般P2：
1、系统的次要功能没有完全实现，但不影响用户使用
2、非主流程的逻辑问题
3、系统业务受到轻微影响
4、操作界面错误（保罗窗口内列名定义、含义不一致）
5、查询错误，数据展示错误
6、删除操作未给提示
7、找不到规律的时好时坏（偶现bug）
8、数据库的表、索引、业务规则、缺省值未加完整性等约束条件
 
四、轻微P3：
1、UI问题（界面格式不规范、页面重叠、不该显示的要隐藏、文字排列不整齐、光标位置不正确、用户体验不友好）
2、文案问题（描述有歧义、错别字、提示语不清楚、提示语丢失）
3、跳转交互问题
4、性能缺陷

### 通过标准

### 提测标准(准入标准)

### 打回标准

### 测试过程限制

## 测试计划

执行几轮？首轮、次轮、回归？冒烟，上线

## 风险识别

进度风险
质量风险

## 效率评估

用例编写、执行效率；
自动化脚本开发、执行、分析效率；
性能脚本开发、执行效率；

# 测试类型

## 性能测试

## 自动化

## 专项

弱网、兼容性、体验等

# 技术&工具

## Python

```python
一行代码
三元运算符( x = 1 if a > 0 else 0)
lambda
生成器表达式
yield
```

### 图形处理

PIL
Opencv

## Groovy

```
执行(
  groovy app.groovy
)
依赖(
  手动，下载jar包放到groovy的lib下
  maven
)
```

## Javascript

## Jmeter

```
命令行参数(
    -Jvar=1  ${__P(var, 2)}
    -n -t app.jmx -l log.jtl
)
内置函数()
内置变量(
    vars.get(name) 只能在线程组内共享，建议优先使用vars，再考虑props
    vars.put(name, val)
    props.get(name) 可以跨线程，建议通过-J、csv、自定义变量等模式变量使用vars
    props.put(name, val)
)
常用元件(
    User Defined Variables
    Http Request Defaults
    Http Header Manager
)
插件管理
脚本代码(
    Jmeter从3.1开始使用groovy作为默认的脚本，且内置了groovy引擎
    HeaderManager
    Header
    DigestUtils(md5)
)
```

### 常用代码合集

```groovy
请求头处理
import org.apache.jmeter.protocol.http.control.HeaderManager;
import org.apache.jmeter.protocol.http.control.Header;
import org.apache.commons.codec.digest.DigestUtils;

HeaderManager headerManager = sampler.getHeaderManager();
String[] headers = headerManager.getHeaders();
log.info("header length: " + headers.length);
for(String header : headers) {
    log.info(header);
}

// 当前时间戳
String timestamp = System.currentTimeMillis();
log.info("timestamp: " + timestamp);

// 获取变量
String sessionId = vars.get("sessionId");
String signature = sessionId + timestamp + "test";
log.info(signature);
// MD5加密
signature = DigestUtils.md5Hex(signature).toUpperCase();
log.info(signature);

// 增加请求头信息
headerManager.add(new Header("signature", signature));
headerManager.add(new Header("timestamp", timestamp));md5加密
一般md5加密会把请求数据也作为加密字符串传入，所以需要特殊处理
import org.apache.jmeter.protocol.http.control.HeaderManager;
import org.apache.jmeter.protocol.http.control.Header;
import org.apache.commons.codec.digest.DigestUtils;

def reqBody = "{\"id\":\"\",\"classifyName\":\"林磊测试\"}";
vars.put("reqBody", reqBody);

HeaderManager headerManager = sampler.getHeaderManager();
String timestamp = System.currentTimeMillis();
String sessionId = vars.get("sessionId");

// 这里使用了md5把请求数据加密
// 上面的reqBody是一个json字符串，注意针对json里面的"需要使用\转义
// http request的body data里面就可以直接使用${reqBody}
// 如果对中文有限制，需要在http request的Content Encoding配置UTF-8
String signature = sessionId + timestamp + reqBody + "skyfire";
signature = DigestUtils.md5Hex(signature).toUpperCase();
headerManager.add(new Header("signature", signature));
headerManager.add(new Header("timestamp", timestamp));随机字符
import org.apache.commons.lang3.RandomStringUtils

// 中文
def chinese = RandomStringUtils.random(5, 0x4e00, 0x9fa5, false, false);
println chinese

// 随机字符，不包含数字
def english = RandomStringUtils.randomAlphabetic(10)
println english

// 随机字符，包含数字
String charset = (('A'..'Z') + ('0'..'9') + ('a'..'z')).join();
String randomString = RandomStringUtils.random(10, charset.toCharArray());
println randomString

// 随机字符，包含数字
def randomString2 = RandomStringUtils.random(10, true, true)
println randomString2Locust
```

## Selenium

## Flask

# 系统知识

http websocket

# 附件&模板

方案、用例、报告等

## 附件1：常用链接

1. [groovy官方](http://www.groovy-lang.org/)

## 附件2：常见问题

### 安装jdk后，没有jre目录

进入jdk安装目录后执行如下命令:
```shell
bin\jlink.exe --module-path jmods --add-modules java.desktop --output jre
```