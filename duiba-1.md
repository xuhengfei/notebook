##兑吧积分商城介绍
兑吧是服务于手机App开发者的积分兑换服务平台。

应用内积分系统能够有效的提升用户活跃度，提升用户体验，使用户更具粘性。

开发者在推出应用内积分系统的同时，却苦于没有丰富的积分兑换项，使积分的使用价值大打折扣，同时打击到用户赚取积分的积极性。

兑吧积分商城致力于提供丰富而又完善的积分兑换选项，比如话费兑换，Q币兑换，支付宝兑换，各种优惠劵，大礼包兑换。还提供诸多积分运营活动，比如大转盘，活动竞猜等等。

丰富的兑换项能极大的提升积分使用价值，外加诸多运营活动工具，能够有效的在应用内提升用户活跃，提升用户体验。

兑吧积分商城接入十分简单，通过App接入SDK，或者嵌入Web网页即可。效果如下：

<img src="http://dui88.qiniudn.com/pdc2unxtx2.png" width="200px"/>
<img src="http://dui88.qiniudn.com/aspva6iiai.png" width="200px"/>
<img src="http://dui88.qiniudn.com/wcaaxq1xs4.png" width="200px"/>

嵌入积分商城后，用户就可以在积分商城内进行各种兑换了。

##积分兑换原理说明

用户在使用积分进行兑换时，兑吧如何与开发者共同来实现这一功能呢？

整体原理图如下：

<img src="http://learnspace.qiniudn.com/snapshot.png" width="400px"/>

当用户发起一个兑换请求时，兑吧服务器会先收到这个请求。然后会依次执行下面的步骤：

1.向开发者服务器发出用户积分余额查询请求

兑吧会向开发者服务器发出用户积分余额查询请求，确保用户有足够的积分来进行兑换活动

2.向开发者服务器发起扣除用户积分的请求

兑吧开始启动兑换流程，向服务器发送扣除用户积分的请求。
比如用户兑换话费需要消耗100积分，这个请求中就会带上用户id，以及需要扣除的积分数：100.
开发者需要对这个请求进行响应，比如扣除成功，或者扣除失败，原因是什么。
只有兑吧收到开发者的扣除积分成功的消息，才会继续兑换流程。

3.兑吧开始进行真实的兑换

4.兑换成功/失败通知

如果兑换成功，兑吧服务器会向开发者服务器发送兑换成功的消息，里面会包含开发者订单号等信息。

如果兑换失败，兑吧服务器也会向开发者服务器发送兑换失败的消息，包含开发者订单号等。
如果开发者服务器收到了兑换失败的消息，开发者需要将此次兑换预先扣除的积分返还给用户

整个兑换过程，开发者需要向兑吧开放3个接口，分别是：

1.用户余额查询接口

2.用户积分扣除接口

3.兑换成功/失败消息的接收接口


整个兑换过程中的请求交互，我们都会进行MD5签名，保证请求的不可伪造，确保资金安全！
