##积分商城介绍
积分商城是一个积分兑换平台，为开发者提供一个积分兑换服务，比如积分兑换话费，积分兑换Q币，积分兑换优惠劵等等。

通过积分商城的兑换服务，为用户提供一个良好的用户体验，可以有效的提升用户的活跃度，增加应用的用户粘性。



##积分兑换商城接入手册
积分商城接入后的执行原理如下图所示
<img src="http://learnspace.qiniudn.com/snapshot.png"/>

开发者通过嵌入积分商城的网页，来完成与积分商城的对接。
整个兑换过程有图中的三个步骤

1.用户在商城网页中提交积分兑换请求

2.商城服务器向开发者服务器提交扣除用户积分的请求

3.扣除成功后，商城进行兑换服务器，成功或者失败后，通知开发者服务器

通过以上三步骤来完成用户积分兑换服务

开发者服务器与商城服务器之间的请求交互需要进行数字签名验证，签名方法我们会提供jar工具，简化此步骤。

综上，开发者需要向商城开放3个接口，分别是：

1.用户积分余额查询接口

2.用户消耗积分接口

3.积分兑换成功失败的通知接受接口


##积分兑换商城，接口规范

1.用户积分余额查询接口

请求示范：http://devsite.com/jifen_query?date=2312343556&uid=123&sign=hihdasd32kng

响应示范：
{"status":"ok","message":"查询成功","data":{"uid":"123","jifen":"100"}}

请求参数说明：  
date:发送请求的时间,long类型的毫秒数  
uid:开发者系统中的用户id  
sign:签名值

响应参数说明：  
整个响应是个JSON字符串  
uid:用户id  
jifen：用户的积分余额


2.用户消耗积分接口

请求示范:http://devsite.com/jifen_consume?date=2837872713&uid=123&quantity=100&description=积分使用说明&sign=jsidfas

响应示范：
{"status":"ok","message":"查询成功","data":{"bizId":"9381"}} 或者  
{"status":"fail","message":"余额不足","data":{}}

请求参数说明：  
date:发送请求的时间，long类型的毫秒数  
uid:开发者系统中的用户id  
description:消耗积分的原因描述  
sign:签名值  

响应参数说明：  
status为ok表示扣除成功  
bizId: 当扣除成功时，积分消耗这一行为的业务订单号(当成功或者失败时的回调，会传回次参数)
status为fail表示扣除失败，并在message上说明失败原因  

3.积分兑换成功失败的通知接受接口

请求示范:http://devsite.com/jifen_notify?date=28973423&uid=123&bizId=2123&success=true&description=兑换成功&sign=jsdjisdf

响应示范:
{"status":"ok","message":"ok"}

请求参数说明： 
date:发送请求的时间，long类型的毫秒数  
uid:开发者系统中的用户id  
bizId:此处兑换积分行为对应的开发者服务器中得业务订单号  
success:兑换行为是否成功  
description:描述  
sign:签名值  


##开发者用户跳转商城首页的免登签名

商城是通过网页url嵌入开发者应用中的，此处需要一个免登操作，让商城知道此用户是属于哪个开发者的哪个用户。

解决方案是通过签名来进行免登。

免登url示范：
http://jifen-store.com/autologin?appKey=xxx&uid=123&date=129832323&redirect=someurl&sign=sdjifdnf

免登成功后，我们会跳转到redirect地址上

免登参数说明：  
appKey:在积分商城网站上分配给你的appKey  
uid:用户id  
date:请求的时间，long类型的毫秒数，30秒过期  
redirect：免登成功后的跳转地址  
sign:签名值  
