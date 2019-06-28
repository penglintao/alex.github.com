---
layout: post
title: "ApiSeverHandler"
description: "ApiServer 流处理"
category: Sample-Posts
tags: [StreamHandler]
imagefeature: 
comments: true
share: true
---

ApiServer的流处理灵活的使用了多态，我们知道一般HTTP处理都使用包含`ServeHTTP`的结构来处理，
一层一层剥开来看，其实都是同一种处理套路

1. 最顶层使用一个`APIServerHandler`直接和底层`http.handler`对接，因为`APIServerHandler`本身也有`ServeHTTP`接口，所以可以对接成功
2. 在`APIServerHandler`的`ServeHTTP`函数中，会进一步操作内部数据对象，比如`FullHandlerChain`
3. `FullHandlerChain`本身也是个`http.handler`的多态对象，也有`ServeHTTP`接口，这个对象的主要目的是操作标准的handler链,比如`MaxInFlightLimit`, `Impersonation`, `Authentication`
4. 
