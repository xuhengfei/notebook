##手机端集成
=======

开发者将兑吧积分商城接入App的过程将非常简单

App中集成兑吧积分商城，需要传入一个商城的入口地址。这个地址需要md5签名，并且带有时间戳，生成的地址在5分钟内有效。

因为这个地址需要签名生成，而且是带有时间戳的，因此需要服务器端来生成。

建议在手机客户端填写一个开发者自己的服务器端地址，开发者服务器端收到请求后，确认用户是在登录状态，即可生成一个签名过的兑吧免登陆地址，并让客户端重定向到该地址。

从而实现客户端用户到兑吧积分商城的免登陆。

###iOS
=======

iOS应用的集成，我们提供兑吧的SDK

SDK下载地址为：https://github.com/duiba/duiba-iOS-sdk/archive/master.zip

下载SDK后，解压文件，里面包含了一个可以直接运行的demo工程

通过修改 CreditViewController中的一行代码，即可运行

	```objective-c
	-(void)enter{
	    //修改这个url地址为 开发者服务器自动跳转的地址
	    NSString *url="http://yourserver.com/auto_login_path";
	    CreditWebViewController *web=[[CreditWebViewController 	alloc]initWithUrl:url];
	    [self.navigationController pushViewController:web animated:YES];
	}
	```
	
解压文件夹下的sdk目录下的文件，就是提供的SDK代码

将所有文件复制到开发者iOS的工程中

参考demo示例，调用sdk即可


###Android
=======




