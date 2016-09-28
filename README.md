# GQWebView
简单H5交互的例子，引用JS库

1，本例用到了JavaScriptCore框架，苹果自身框架，功能强大，只用了其中一个JSContext就完成了简单交互，若要完成复杂交互还要深入研究；
2，iOS8以后苹果完善了网页框架，使用了新的WebKit框架，确实弥补了一些不足，WKWebView取代了UIWebView，但为了使用更多的系统需求，开发中不少还是从iOS7做起的，开发中以情况，交互量而定；


//    返回的H5方法

    //js方法名＋参数
//    NSString* jsCode = @"history.go(-1)";
    
    //调用html页面的js方法
//    [webView stringByEvaluatingJavaScriptFromString:jsCode];

    
//    documentView.webView.mainFrame.javaScriptContext 获取context的固定写法。
    _context=[webView valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
    //获取首页返回键的方法，
    _context[@"home"] = ^(){
        [[[UIAlertView alloc] initWithTitle:@"恭喜！" message:@"截取到了返回的方法，在这里可以返回我们自己的页面！！！" delegate:nil cancelButtonTitle:nil otherButtonTitles:@"好的", nil] show];
        
        
//        方法带参数时获取方法参数
        NSArray *array = [JSContext currentArguments];//H5方法里的参数
        NSString *url = [array lastObject];
        //        NSString *urlGame = [url substringToIndex:url.length].description;
        NSLog(@"%@, %@", array, url);
    };
    
    
    if (self.navigationController) {
//        获得H5标题作为页面title。
        self.navigationItem.title = self.title?:[_webView stringByEvaluatingJavaScriptFromString:@"document.title"];
    }
