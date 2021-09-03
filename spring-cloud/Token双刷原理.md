# Token双刷原理

为了解决上述 token过期了**活跃**用户需要在登录页面重新登录 

#### ‘活跃用户’

在 access_token创建开始时间点 到 2*access_token实效 的 时间内认为用户是活跃的。







refresh_token 的有效时间 >= 2 * access_token 的有效时间

一般,refresh_token 的有效时间 > 2 * access_token 的有效时间
比如，access_token 实效7天，那么 refresh_token 实效可以给15天,也可以给30天
当然，access_token和refresh_token 的时长具体多少，需要根据环境决定，如涉及到金钱的 银行客户端，12306客户端等 token时长都很短，而普通app客户端的token可以是几天甚至上月.





**刷新refresh_token**
每次 刷新access_token 时判断 refresh_token 是否快过期 [ refresh_token 剩余有效时间 <= 2*access_token实效]，如果是，那就连refresh_token 也刷新。

服务器端判断的，前端传参access_token，服务器端知道这个是否过期了，返回通知前端，前端然后用refresh_token去重新获取access_token，如果服务器端判断refresh_token也过期了，就通知前端你需要重新登录了







传入 refresh token，鉴权服务器验证 refresh token 是合法的之后，返回一个新的 access token。这样，当 access token 过期后，使用方就使用 refresh token 来获取一个新的 access token。

 

　　问题来了，这样做难道不会破坏安全性吗？前面说 access token 可能会泄漏，于是设置较短的有效期，可是现在又同时给一个 refresh token，那 refresh token 是怎么保证安全的呢？　　

　　答案是，为了 refresh token 的安全，Oauth2.0 要求，refresh token 一定要保存在使用方的服务器上，而绝不能存放在移动 app、PC端软件、浏览器上，也不能在网络上随便传递。调用 refresh 接口的时候，一定是从使用方服务器到鉴权服务器的 https 访问。所以，refresh token 比 access token 隐蔽得多，也安全得多。当然，这需要使用方正确的遵守 Oauth2.0 的要求。