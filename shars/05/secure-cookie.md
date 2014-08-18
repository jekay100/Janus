#Cookie安全

[name][value][domain][path][expires][httponly][secure]

##子域cookie机制 [domain]

* 不指定时设置到当前域
* 可以显式指定为当前域
* 可以手工设置为父域
* 不能设置成外域
* 不能设置成同级域
* 不能设置成子域

##路径cookie机制 [path]

* 不指定时设置到当前路径
* 可以指定到任意路径
* js只能访问当前路径下的cookie
* 可以使用iframe穿透路径机制的限制

##httpOnly cookie机制 [httponly]

* js无法读写
* 服务器端泄漏

##secure cookie机制 [secure]

* 只有在https协议中传输
* js可以读写

##本地cookie与内存cookie

* 没有设置expires为内存cookie
* 设置了expires为本地cookie
* js可以通过为内存cookie指定expires将内存cookie变成本地cookie

##P3P cookie

* Platform for Privacy Preferences
* ie默认不允许第三域通过加载而设置另一方域的cookie
* 如果响应头P3P字段，就可以设置第三域的cookie
* 通过P3P设置的cookie拥有P3P属性
* 发送的cookie如果是内存cookie则都会发送
* 发送的cookie如果是本地cookie则只有带有P3P属性的cookie会发送
