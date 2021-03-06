### OAuth流程

OAuth是一种安全的授权框架，提供了一套详细的授权机制。用户可以通过接口，授权第三方应用访问特定的资源。

1.__用途__

减少用户的注册，避免创建大量账户； 同一系统的各个产品可以共用一套用户体系等

2.__涉及到的角色__

__授权服务端应用（Authorization Server）__：服务提供商提供的专门用于处理授权的服务端应用，比如上面介绍的QQ登录、微博登录，当然也可以搭建自己的授权服务端。

__资源服务应用（Resource Server）__：服务提供商存放用户及其他资源的应用，一般用于接口的形式返回第三方应用请求的资源。它可以与授权服务端属于同一个应用，也可以分别属于不同的应用。

__用户（User）__：用户在授权服务端登录，授权服务端记录了用户的账户体系。当然，有的网站会在你通过第三方账号第一次登录成功后，要求绑定你的手机号并创建昵称，这就是他们在创建自己的账户体系（跟OAuth2.0协议无关，这里不作展开）了。

__接入的第三方应用（Third-party Application）__：接入认证的第三方应用又被称为“客户端”，比如一个普通的网站、APP。


__3.几种授权模式__

__授权码模式（authorization code）__：这是功能最完整，流程最严密的模式。现在主流的使用OAuth2.0协议授权的服务提供商都采用了这种模式，我在下面举例也将采取这种模式。

    （A）用户访问客户端，后者将前者导向认证服务器。

    （B）用户选择是否给予客户端授权。

    （C）假设用户给予授权，认证服务器将用户导向客户端事先指定的"重定向URI"（redirection URI），同时附上一个授权码。

    （D）客户端收到授权码，附上早先的"重定向URI"，向认证服务器申请令牌。这一步是在客户端的后台的服务器上完成的，对用户不可见。

    （E）认证服务器核对了授权码和重定向URI，确认无误后，向客户端发送访问令牌（access token）和更新令牌（refresh token）。


__简化模式（implicit）__：跳过了请求授权码（`Authorization Code`）的步骤，直接通过浏览器向授权服务端请求令牌（`Access Token`）。这种模式的特点是所有步骤都在浏览器中完成，`Token`对用户可见，且请求令牌的时候不需要传递`client_secret`进行客户端认证。

    （A）客户端将用户导向认证服务器。

    （B）用户决定是否给于客户端授权。

    （C）假设用户给予授权，认证服务器将用户导向客户端指定的"重定向URI"，并在URI的Hash部分包含了访问令牌。

    （D）浏览器向资源服务器发出请求，其中不包括上一步收到的Hash值。

    （E）资源服务器返回一个网页，其中包含的代码可以获取Hash值中的令牌。

    （F）浏览器执行上一步获得的脚本，提取出令牌。

    （G）浏览器将令牌发给客户端。

__密码模式（resource owner password credentials）__：用户向第三方客户端提供自己在授权服务端的用户名和密码，客户端通过用户提供的用户名和密码向授权服务端请求令牌（`Access Token`）。

    （A）用户向客户端提供用户名和密码。

    （B）客户端将用户名和密码发给认证服务器，向后者请求令牌。

    （C）认证服务器确认无误后，向客户端提供访问令牌。

![Image](https://img-blog.csdn.net/20150507184751944?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1Y2h1bm1pbmcwMzM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

![Image](https://user-gold-cdn.xitu.io/2018/9/3/1659da92f23c13fa?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

 
__4.主要流程__

1. 客户端请求授权服务器，获得授权码（authorization code）

2. 客户端通过授权码（authorization code）再次请求服务端，获得token（authorization token）

3. 客户端通过Token获得用户信息

### 链接

* [使用Python实现OAuth2.0认证服务器](https://blog.csdn.net/liuchunming033/article/details/45564791)

* [JWT和Oauth2的区别和联系](https://www.jianshu.com/p/1870f456b334)

* [OAuth2.0协议入门（二）：OAuth2.0授权服务端从设计到实现](https://juejin.im/post/5b8cb6586fb9a01a133685c9#heading-2)

* [理解OAuth 2.0](https://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html)

* [理解 OAuth 2.0 认证流程](https://lotabout.me/2020/OAuth-2-workflow/)