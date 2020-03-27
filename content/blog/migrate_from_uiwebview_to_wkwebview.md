---
title: "ITMS-90809: Deprecated API Usage - Migrate from UIWebview to WKWebView"
date: 2020-03-27T21:37:30+08:00
draft: false
author : "Nour Araar"
categories : ["Development"]
tags: ["uiwebview","wkwebview"]
description : "If you are an IOS developer and you are using UIWebView and constantly deploying apps to the app store that mean you definitely faced a warning from apple telling you"
featured : "cover.jpg"
featuredalt : "Migrate from UIWebview to WKWebView"
featuredpath : "img/migrate_uiwebview"
linktitle : "Migrate from UIWebview to WKWebView"
type : "post"
---

If you are an IOS developer and you are using UIWebView and constantly deploying apps to the app store that mean you definitely faced a warning from apple telling you

    ITMS-90809: Deprecated API Usage - Apple will stop accepting submissions of
    app updates that use UIWebView APIs starting from December 2020. 
    See https://developer.apple.com/documentation/uikit/uiwebview for more information.


That mean you should start to get rid of all the uiwebview and replace them with WKwebView.  
And you will not be able to submit any app using uiwebview starting from Aprile 2020

**So How you will do it**  
First if you are using it in your code all you have to do is to start migrating from **UIWebView** to **WKWebview**  

you need to replace this code 
```swift
import UIKit

class TestViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        let webView = UIWebView()
        let request = URLRequest(url: URL(string:"https://google.com")!)
        webView.loadRequest(request)
    }
    
}
```

with this code 
```swift
import UIKit
import WebKit

class TestViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        let webView = WKWebView()
        let request = URLRequest(url: URL(string:"https://google.com")!)
        webView.load(request)
    }
}
```

migrating from **UIWebView** to **WKWebView** might seem quite straightforward, but you probably use some 3rd party libraries and they might also contain UIWebView.  
You need to find all of them and update them, if available, or replace them. This process is not exactly trivial.
If you use **3rd party** libraries as code, for example via **Cocoapods**, you can just do a text search for **UIWebView** in their sources.

one of the most using library is **RxSwift** using the **UIWebView** in version prior to **5.1.0**  
so you can use this command to find all of these libraries

    grep -r 'UIWebView' .




Then check the result that you got and try to upgrade all the pods and that’s it 

