##接口集成

<img src="http://learnspace.qiniudn.com/snapshot.png" width="400px"/>

兑吧与开发者服务器的交互原理如上图所示

开发者需要向兑吧开放3个接口，分别是：

1.用户余额查询接口

2.用户积分扣除接口

3.兑换成功/失败消息的接收接口

所有的请求都会使用md5进行签名，在开发前，你需要先获得AppKey和AppSecret。
AppKey可以在我的应用中找到，AppSecret可以在我的应用->应用信息 中找到，通过邮件方式获取AppSeret。
请务必保管好AppSecret,泄露AppSecret可能会导致你的账号资金被盗。

我们为不同的服务器编程语言开发者提供了不同的SDK,以方便开发者更高效的接入我们的服务。

1.用户余额查询接口

Java语言  |  PHP语言  | .Net语言

```java

CreditTool tool=new CreditTool("appKey", "appSecret");
                           
try {
    CreditQueryParams params= tool.parseCreditQuery(request);//利用tool来解析这个请求
    String uid=params.getUid();//用户id
    Integer credits=queryUserCredits(uid);//查询用户的积分，此处需要开发者自行实现
    CreditQueryResult result=new CreditQueryResult(true, credits);
    response.getWriter().write(result.toString());
} catch (Exception e) {
    // TODO Auto-generated catch block
    e.printStackTrace();
}

```

2.用户积分扣除接口

Java语言  |  PHP语言  | .Net语言

```java
xxx
xxx
xxx

```

3.兑换成功/失败消息的接收接口

Java语言  |  PHP语言  | .Net语言


```java

xxx
xxx
xxx

```


所有的请求进行md5签名，确保传输的安全可靠。

md5签名的原理如下：

将所有的参数与 appSecret按哈希值升序进行排列。
Md5(value1+value2+...appSecret...+valueN),appSecret 在签名中的顺序取决于他在所有参数名中的哈希值排列的顺序。
例：appKey：testappkey，appSecret：testsecret
参数列表：
{appKey=testappkey,timestamp=129832323,redirect=someurl}
签名原串：testappkeytestsecretsomeurl129832323
签名后字符串：9318d5b6fee1e9ce823b3f6b431bc371
自动登录url:
http://www.dui88.com/autologin?appKey=testappkey×tamp=129832323&redirect=someurl&sign
=9318d5b6fee1e9ce823b3f6b431bc371


更多接口

审核接口

很多设计金钱的兑换项，出于安全的考虑，需要通过审核通过后才能进行兑换。兑吧也支持Api接口的批量审核功能。

当某笔兑换需要审核时，我们在向开发者服务器发起扣除积分的请求中，会说明此笔兑换是否需要审核。
如果开发者收到请求需要审核，可以将此订单打上标记。
后续通过自己的后台页面进行审核操作。审核通过或者拒绝，可以通过批量接口向兑吧服务器发起审核请求。

审核接口使用：

Java语言  |  PHP语言  | .Net语言

```java
xxx
```

