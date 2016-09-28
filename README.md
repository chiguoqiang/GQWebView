# GQWebView
简单H5交互的例子，引用JS库
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
