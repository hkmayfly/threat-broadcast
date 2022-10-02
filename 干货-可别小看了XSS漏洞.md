对于初了解xss漏洞的人来说，XSS漏洞的危害就是获取受害者的cookie，来进行 ‘cookie劫持’。

今天就总结一下XSS漏洞的危害性，望安全人员不要轻视，开发人员不要忽视

##  **XSS漏洞简介**

XSS攻击通常指黑客通过“HTML注入”篡改网页，插入恶意脚本，从而使用户浏览网页时控制用户浏览器的一种攻击。例如：

  * 

    
    
    <p>a</p>

如果我能控制a，将a改为`</p><script>alert("1")</script><p>`,这个地方的代码就会变成这样:

  *   *   * 

    
    
    <p></p>      <script>alert("1")</script>      <p></p>

就会执行script脚本，这么想我们是不是能篡改网页html文件，来让他执行我们的语句？

##  **第一 cookie劫持：**

如果网站存在XSS漏洞，可以通过XSS漏洞来获取用户的cookie危害：利用用户的cookie来进行登录用户后台payload：`<script>alert(document.cookie)</script>`

##  **第二 构造GET或POST请求:**

黑客可以通过XSS漏洞，来使得用户执行GET或POST请求危害：可以控制用户删除数据或者发送邮件例如GET payload：

  * 

    
    
    <script>window.location.href='////www.xxx.com/index.php?type=delete&id=1';</script>

POST请求 需要线创建一个表单，然后让表单自动提交信息。

##  **第三 钓鱼**

我们从一开始的XSS漏洞简介可知道，XSS漏洞可以让我们对网页进行篡改，如果黑客在登录框的地方把原来的登录框隐藏一下，自己伪造一个登录框，用户在登录框上输入账号密码就会传送到黑客的服务器上危害：获取用户账号密码

## 第四 识别用户浏览器

通过script语句能获得用户的浏览器信息危害：获取浏览器信息，利用浏览器漏洞进行攻击payload：`<script>alert(navigator.userAgent)</script>`![](https://tix-article-1254423997.cos.ap-beijing.myqcloud.com/wx-article/pic/3d35f470425e11edbbdf145afc1fa588.png?q-sign-algorithm=sha1&q-ak=AKIDY3PcgZnyb5PXUGyIbjhgfYLGD5rX4g6V&q-sign-time=1664720745%3B3241520805&q-key-time=1664720745%3B3241520805&q-header-list=host&q-url-param-list=&q-signature=054ad589111b87634f8650894e5ec8742052e5be)

##  **第五 识别用户安装的软件**

通过script语句能够识别用户安装的软件危害：获取用户软件信息，利用软件漏洞进行攻击如下代码：

  *   *   *   *   *   * 

    
    
    try{     var Obj=new ActiveXObject('XunLeiBHO.ThunderIEhelper'); }     catch(e){         //异常     }

##  **第六 获得用户真实ip地址**

借助第三方软件,比如客户端安装了Java(JRE)环境,那么可以通过调用JavaApplet接口获取客户端本地IP

##  **第七 判断用户是否访问某个网站**

style的visited属性,访问过的链接,颜色会变化.

##  **第八 蠕虫**

用户之间发生交互行为的页面,如果存在存储型XSS,则容易发起XSS
Worm攻击.如：2003年的冲击波蠕虫，利用的是Windows的RPC远程溢出漏洞还有百度空间蠕虫，可自行百度搜一下

##  **XSS绕过方式**

  * JS编码
  * HTML编码
  * URL编码
  * 长度绕过
  * 标签绕过(标签闭合,标签优先性)
  * window.name利用
  * Flash XSS
  * 利用Javascript开发框架漏洞
  * 利用浏览器差异
  * 关键字、函数 **XSS防护方法**  

  * 过滤输入的数据,非法字符
  * 对数据进行编码转换
  * 添加HttpOnly
  * 输入合法性检查
  * 白名单过滤标签
  * DOM XSS防御

作者：codingnote来源：https://codingnote.cc/p/696976/ **加个好友进技术交流群**
**请备注：进群**![](https://mmbiz.qpic.cn/mmbiz_jpg/bMyibjv83iavzf2RrhsWpwMic7OoaXePbDicXicOGAZh3OPcYicGo75JnCFI4pxLciazS3EXPnkO6Ps3bktDKk3v3w3hQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)  
 **推荐阅读**  
[![](https://mmbiz.qpic.cn/mmbiz_png/bMyibjv83iavxQd7OoTPN1n5RYZFuD1wepiaJIuWfTVpBpuDOF8kNpwAnCWQrYrUjrH6M9efA40sVoHjNjIsbuN5g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247507486&idx=1&sn=4d998d84f193d11c0e18c8ad19a20357&chksm=9acd0e81adba87974fb1069997890d93ae546d5586f6dd27423273934779e304ceef421c800b&scene=21#wechat_redirect)

欢迎  **在看** 丨 **留言** 丨 **分享至朋友圈**  三连

  

 好文 **推荐  ** ** **

  

  * # [ 实战杀猪盘渗透测试](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247509036&idx=1&sn=78884a2be9da5b35d4064634f9382c60&chksm=9acd74b3adbafda525ed2b38eaee333d14cf39a3cfaf687aa2e1983f7006040dd4c90e0e7386&scene=21#wechat_redirect)

  * [实战|一次不太成功的反诈骗渗透测试](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247508373&idx=1&sn=abd62618884e05c3765319cda22cf9a2&chksm=9acd710aadbaf81ccc98724a9374586c53c9b282104137f7c5cc9226a970ebc1eee77d62f296&scene=21#wechat_redirect)
  * [CTF常用脚本工具（附下载地址）](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247508323&idx=1&sn=fe5df5b7517f40356b7d5efd60dfa315&chksm=9acd71fcadbaf8ea7c5bdaa64e4336d9a540b0b52cf53c637b630463a65964d62d727312bbd8&scene=21#wechat_redirect)
  * [实战|一次对BC网站的渗透测试](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247508301&idx=1&sn=b8ff47fb088d98e973011ace8e9b9707&chksm=9acd71d2adbaf8c4d44838a3740da596ae4a35dac0a5eb65e403f3f6fed4255ad740deded980&scene=21#wechat_redirect)  

  * [实战|文件上传绕过的一次思路总结学习（两个上传点组合Getshell）](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506925&idx=1&sn=f4647119489b6e980d3a465fb7069c89&chksm=9acd0b72adba82644aeb5fa5471593429f168a234bba82a427c633e2a8f3f29fa9927529836f&scene=21#wechat_redirect)
  * [AppScan10.0.8（附下载地址）](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506936&idx=2&sn=08f047e6ce611b84d0b277e846149ca6&chksm=9acd0b67adba82716022cad5f5a38b5e5e29d26dc34b43814e7d29895ebbea5f4aab01fd6cd1&scene=21#wechat_redirect)
  * [BurpSuite_pro_v2022.8（附下载地址）](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506862&idx=2&sn=756e9f1c42caa20cb8c87719e102f1c5&chksm=9acd0b31adba822768004df53a031be56ff588d99f9ac34c1efcf61f4108d7e3112148754e5a&scene=21#wechat_redirect)  

  * [一款强大的红队资产测绘工具](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506822&idx=1&sn=bdd3454c4d6cf88452e1b2756ffeece2&chksm=9acd0b19adba820f7e729419ee8daac6f9e3c1f240610102f0e5cb485d459163729ddaf041fa&scene=21#wechat_redirect)
  * [红队必备-防蜜罐抓到被打断腿](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506528&idx=2&sn=ef3e0dfd2e5d31896db7f7e1c93fdb26&chksm=9acd0affadba83e9ea3d46e31cc6ff3055862d9e483442f8664ff5f2907ec220dcfeb9aa2bc6&scene=21#wechat_redirect)  

  * [HVV之内存马检测工具](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506511&idx=1&sn=3a179572f47e4c2aa9a895e1b4688779&chksm=9acd0ad0adba83c649979a6f5e99074b5beab880a395e81dd2948a8de0d33f3c9584c21bed54&scene=21#wechat_redirect)
  * [HVV中一种针对红队的新型溯源手段](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506457&idx=1&sn=fe2fc4cf69cf93e518a3b35a4d67fcd1&chksm=9acd0a86adba8390f7fdaaa09af9092330eeae7c9d6bef4ccca1c0defd3d7019fdd946d46cb9&scene=21#wechat_redirect)
  * [HVV|蓝队防猝死手册](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506444&idx=1&sn=fc554a56ca839dda6cd66a10ae6e09f8&chksm=9acd0a93adba8385a48d911bbce1de4d85f8caa77a927c285e9fdf7e59d3c377aa918938a050&scene=21#wechat_redirect)  

  * [蓝队/红队钓鱼项目（附分析报告）](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506431&idx=1&sn=0a2f549d98e107ce3215745e83ab05ef&chksm=9acd0960adba80769e60a58ca8fd44f49bfc2f0368003f88a60637d4566ca3ee836265205668&scene=21#wechat_redirect)
  * [红队防猝死手册](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506396&idx=1&sn=aecdbe3fcc1d53071fb6dd78465476d9&chksm=9acd0943adba805558c5dc68656e7299982559ac96714f5a38655640b9545e8f180e67b7baf8&scene=21#wechat_redirect)
  * [干货|红队全流程学习资料（附下载地址）](http://mp.weixin.qq.com/s?__biz=MzAwMjA5OTY5Ng==&mid=2247506343&idx=1&sn=8c33f345f0204b4d97aed87c560318fa&chksm=9acd0938adba802e3c215f9fa1f5b0b290bcf90705775fe7944110e806def703df0a7517eab1&scene=21#wechat_redirect)

![](https://mmbiz.qpic.cn/mmbiz_jpg/bMyibjv83iavyqK2PI61AISe8Xo9DlXP6vgLIhLck2JkmPSmyDWxKQEwdqBeKmibz0BhQDyTaE8Kpw3OPuYgCaHEA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

