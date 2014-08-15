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



