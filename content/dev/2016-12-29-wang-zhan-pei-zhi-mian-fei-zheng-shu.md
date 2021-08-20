---
title: 网站配置免费证书
author: Carlxu
type: post
date: 2016-12-28T11:47:31+00:00
url: /201612/224/
categories:
  - 专业笔记
tags:
  - wordpress

---
## 申请免费SSL证书（提供泛域名支持） {#toc_0}

申请流程：  
（1）申请CSR文件  
（2）申请证书  
（3）阿里云虚机配置。CDN  
（4）域名解析配置  
（5）wordpress的配置  
<!--more-->

### 1. CSR文件。 {#toc_1}

域名邮箱或者whois邮箱（不能带whois保护），同时域名邮箱也有相应的要求  
（必须是相应的管理类邮箱 <admin@xxx.com>/<webmaster@xxx.com>），可以使用QQ的域名邮箱  
CSR证书比较简单，自行生成或者在线生成，推荐使用在线生成：直接贴地址：  
<https://www.chinassl.net/ssltools/generator-csr.html>  
提醒：记得申请的时候一定要选中最下面的发送邮箱选项，会发送到你的邮箱，或者申请完成后手动在页面下载。  
![][1] 

### 2. 申请证书 {#toc_2}

地址：[loovit][2]  
打开页面之后，复制粘贴CSR文件内容进去，全部（begin end部分也要带）  
email地址最好是写管理类的域名邮箱，不然后面还得验证。

下面的姓名电话可选，没有太大意义。强迫症患者你就写上吧。  
点击verify按钮，稍等几秒弹出提示：你提供的CSR属于xxx.xxx.com域名，检查下是否正确。  
点击确定，稍作等待后进入验证邮箱界面，选择一个你可以正常使用的域名邮箱地址，提示成功后，稍等接收邮件！

![][3]  
很快邮件就办下来了，点击链接批准，又回收到一封申请成功的邮件，邮件最下方包含证书的crt，后面会用到。  
![][4]  
1、2封邮件都有重要作用（1.申请CSR的时候发送的邮件；2.证书申请成功的邮件）  
CSR邮件中的privatekey部分在证书安装的时候需要用到，切记要保存；  
证书申请成功邮件最下面以文本形式发给你的也要保存；

### 阿里云虚机配置 {#toc_3}

证书做好了之后，我们把它配置到阿里云虚机，这个云虚机其实是不支持https的。但是如果购买了CDN的话，是可以支持的。为此我开通了CDN，选的是按流量收费。

访问阿里云的管理后台，进入CDN管理控制台， 域名列表->添加新域名, 源站域名选择IP, 这个IP可以在云虚机的控制台主机信息里找到。 这也是使用CDN的好处之一，可以隐藏源站IP，一定程度减少了被DDos的可能性，其他信息类似如下填写，注意这里的端口一定要使用80。因为云虚机的443端口（https默认端口）不开放，我们只能访问CDN服务器的443端口，然后由CDN服务器回源到云虚机的80端口，这样就实现https的访问，从本质上来说CDN网络节点就是一连串的反向代理服务器。  
![][5] 

云虚机是阿里云旗下的（收购的万网业务），很快就通过审核，或者说不用审核，毕竟自家的，如果你使用别家的服务器可能需要一段时间审核。  
![][6]  
点击立即配置，把https安全加速打开，打开证书配置。找到申请证书邮件里的。打开并复制其内容到阿里云CDN的“证书管理”，里“证书内容”输入框。再找到刚才我们生成csr证书，把它的内容也复制出来，放到“私钥”的输入框。跳转类型选择http->https，这样更利于SEO, 因为这样可以把相似或相同的内容集中到同一个url，避免了权重分散。  
![][7] 

配置完成是这个样子，为何配了两个，一个带www和不带www的，因为我还没搞定不带www如何解析跳转到带www的地址，所以配了两。  
![][8] 

### 域名解析配置 {#toc_4}

接下来我们配置CNAME绑定,阿里云会分配CDN的域名给你，比如像我的这样，你要在DNS里更改域名的映射  
我的域名是万网的，现在也归并到阿里云了，更改如下：  
![][9]  
因为没搞定不带www如何解析跳转到带www的地址，暂时先这么配，而且CNAME和MX的@配置冲突，现在暂时没法用我的域名邮箱了，这个后面再看有什么办法解决吧。。。

### WordPress配置 {#toc_5}

最后一步是修改站点的代码，前面说过，虽然用户通过https访问CDN服务器，但CDN服务器到源站是通过http访问的，（以WordPress为例）这样的话，呈现在最终用户的页面中里，链接的地址还是显示http开头的，比如：<http://www.carlxu.cn/about> 我们需要呈现给用户的是<https://www.carlxu.cn/about> 这种的url, 在WordPress也很简单，它是有一套专门的url函数，可以做一些url控制，比如rewrite等，这也是不要去硬编码url的原因， 跟踪代码可以发现，它是通过 $_SERVER[‘HTTPS’] 服务器变量判断当前环境是否为https访问，我们可以这样骗过它，在wp-config.php文件开头写入以下内容：

<pre><code class="language-php">define(‘WP_HOME’, ‘https://’.$_SERVER[‘HTTP_HOST’]);
define(‘WP_SITEURL’, ‘https://’.$_SERVER[‘HTTP_HOST’]);
$_SERVER[‘HTTPS’] = ‘ON’;
</code></pre>

站内链接支持  
你在上传到空间的附件都被 WordPress 标记为了绝对链接，而且全都妥妥的写入了 “http://”。一般来讲，是需要用数据库替换的，不过这种方法有点小危险，我这里给你推荐另外一个不错的选择：使用代码让 WordPress 在加载附件之前将链接替换就好了！  
（我希望你使用了 WordPress 的子主题功能……）

找到当前主题下的 function.php 文件，编辑之，在里边代码的末尾追加如下代码：

<pre><code class="language-php">/* 替换图片链接为 https */
function my_content_manipulator($content){
    if( is_ssl() ){
        $content = str_replace('http://www.logcg.com/wp-content/uploads', 'https://www.logcg.com/wp-content/uploads', $content);
    }
    return $content;
}
add_filter('the_content', 'my_content_manipulator');
</code></pre>

另外，除了这个大头意外，你还需要关心站内的各种内链：

修改“菜单”当中的所有“自定义链接”为相对路径；  
修改“设置”→“常规”里的“站点地址”和“WordPress 地址”为 HTTPS；  
修改其他自己手贱写入的绝对链接地址……  
关心一下插件

### 这下，你的博客应该已经能够完美的显示出一个绿色的小锁啦！ {#toc_6}

![][10] 

<!--### 其他说明 搜到的其他配置，可以不用看了，先保存着。 #### 合并文件 证书的安装，因为我们的web端是tomcat架设的，查了下相关证书的配置文档和博文，发现也就是p12类型的比较好弄 所以这里就暂定了使用.p12证书的方式来更换证书 - 准备文件： 2个crt ：一个是csr邮件中的crt，一个是证书申请下来邮件最下方的begin开头，end结尾crt。 1个key ：csr邮件中的key 以上三个文件放在同一个文件夹中，题外话：这三个文件不能直接用的，需要合并之后才可以正常使用 - 合并步骤： 1、生成有效的pkcs12文件： （1）打开终端命令行； （2）进入crt和key文件所在文件夹； （3）执行命令：cat key.key xxx1.crt xxx2.crt > xxx.pem (首先将三个文件合并，生成一个.pem文件)
（4）执行命令：openssl pkcs12 -export -in xxx.pem -passin pass:0537xxx -out xxx.com.p12 -passout pass:0537xxx
//  最后我们看到的xxx.com.p12文件   切记：0537xxx  是设置的密码，后面设置的时候需要用到，自己记住。
（5）keytool -list -rfc -keystore xxx.com.p12 -storepass 0537xxx 输出下文件内容，确保不会出错。

提醒：在执行第四步操作的时候很可能会出错
nginx: [emerg] PEM_read_bio_X509_AUX("/root/domain.crt") failed (SSL: error:0906D066:PEM routines:PEM_read_bio:bad end line)
是因为我们在合并crt和key文件的时候有分隔符出现问题。
使用你的文本编辑器打开xxx.pem（第三步合并后的文件），你会发现，每个end和之后的begin合并在了一行，默认end后面是5个-然后回车换行的。
这里直接从end和begin之间的----------中间硬回车，问题解决。
实际第五步如果执行成功，这个P12文件已经是可以正常使用的了。

#### 安装证书
下面就是简单的tomcat如何配置https SSL证书的问题了。百度一堆教程，这里不做过多的解释，直接上操作步骤

（1）将生成好的.p12文件上传到阿里云esc服务器的tomcat目录下面  scp  /usr/xxx/xxx.com.p12 root@xxx.xxx.com:/server/tomcat/ (scp命令如何使用自己百度)
（2）ssh连接阿里云服务器，进入服务器tomcat目录
（3）命令行操作：vi conf/server.xml
（4）找到以下代码

```
<Connector port=&quot;443&quot; protocol=&quot;org.apache.coyote.http11.Http11Protocol&quot; SSLEnabled=&quot;true&quot; maxThreads=&quot;150&quot; scheme=&quot;https&quot; secure=&quot;true&quot; clientAuth=&quot;false&quot; sslProtocol=&quot;TLS&quot; keystoreFile=&quot;server/tomcat/xxx.com.p12&quot; keystoreType = &quot;PKCS12&quot; keystorePass=&quot;0537xxx&quot;/>
```
在这里设置下keystoreFile：.p12文件具体地址（注意：阿里云貌似需要全路径）
keystoreType：文件类型：PKCS12
keystorePass：证书密码，合并步骤34中你输入的密码

基本搞定，结束编辑，保存，退出，重启tomcat！！！！

#### 开启访问 HTTPS 301重定向

细心的你这时候一定会发现，你的网站这时候虽然支持了 HTTPS 访问，但是似乎也可以使用 HTTP 来访问，考虑到搜索引擎目前收录的都是你的 HTTP 链接，那么如果不做点什么的话恐怕这张 SSL 证书将会毫无用处！

我希望你的空间能够支持  .htaccess ，如果你的博客开启了伪静态的话，那八成你的空间是支持的。 ：）

我们使用  .htaccess  文件来添加一个301重定向（其实还有其他各种迁移的办法，但是谷歌大爷官方推荐使用301重定向）将所有的 HTTP 流量使用301重定向到 HTTPS 上边去，当然，这样还有一个潜在的问题：国内百度等搜索引擎的爬虫不支持 HTTPS！

我很好奇，为什么在全世界都提倡 SSL Everywhere 的情况下，我国国内的互联网环境还是“明文走天下”，当然，这可能也跟那个“Girl Friend Wall”有关系吧……（不然不好和谐了啊~）所以，我们还要单独为国内的一些搜索引擎的爬虫定制一下规则，如果检测到他们的 UA，那么就允许他们访问 HTTP 流量。

在你博客空间的  www  目录（有的可能是  public_html ）下，找到 .htaccess 文件，编辑它，在里边填入下列代码：

#### 网站定制化开启 HTTPS 的301重定向
RewriteCond %{SERVER_PORT} !^443$
RewriteCond %{HTTP_USER_AGENT} !MSIE/[1-8]\. [NC]
RewriteCond %{HTTP_HOST} www.logcg.com
RewriteRule ^.*$ https://www.logcg.com%{REQUEST_URI} [L,R=301]
对了，考虑到巨硬的 IE 大爷，我们把12345678都排除在外，让它们妥妥的滚去访问 HTTP 吧，省的各种警告烦心。

三、开启登录和后台的强制 SSL

虽然有了整站的重定向，但我们不妨还是将 WordPress 本身自带的功能打开，以期更完善的兼容体验——毕竟是301重定向。
还是找到你网站根目录里边，这次要修改的文件是 config.php，直接在这个文件的末尾另起一行，追加两行代码：

/* 强制后台和登录使用 SSL */
define('FORCE_SSL_LOGIN', true);
define('FORCE_SSL_ADMIN', true);
四、站内链接支持

五、关心一下插件

现在，还剩下最后一个问题：插件的兼容性！

是的没错！并不是所有的插件都会兼容 SSL！（尤其是国内的插件）

对了！关于 CNZZ 这个统计的话你只需要改动一下统计代码就可以，将 HTTP 修改为 HTTPS 即可。不过国内比较常用的 JiaThis 社会化分享插件就无力了，只能割爱停删。

另外，曾今“我爱水煮鱼”开发的相关文章插件：WordPress Related Post，后来卖给了老外，总是会加载一个站外的链接，如今还因为 Girl Friend Wall 的问题导致这个 js 脚本各种菊花，只好果断停删。

你可以使用任意浏览器，打开你的博客页面之后随便打开一篇文章，选择类似于“检查元素”的操作，查看报错就可以了：要求是没有任何红色的错误，黄色的警告“⚠️”可以忽略。

关于删除的插件那功能怎么办？

当然是找替换插件了，这里针对如上的两个插件，路由推荐两个插件：

anyShare 它是一个功能简洁十分轻量级的社会化分享插件，按钮比较大（你可以稍后在这片文章末尾看到样式），虽然说它已经10个月没有更新，但我向你保证这玩意儿绝对兼容最新版本的 WordPress 并且功能完美。：）
Yet Another Related Posts Plugin 这个是另外一个相关文章插件，再也没有烦人的站外链接了，免费版功能足够，而且同样支持RSS，而且现在它的配置界面也不再那么让人望而生畏，对了！虽然它同样被提示不兼容最新版——但我保证，这玩意儿同样功能正常~
最后，你可以到这个页面来参考落格都使用了哪些狂拽炫酷吊的 WordPress 插件，这些插件至少都会兼容 SSL 。

这下，你的博客应该已经能够完美的显示出一个绿色的小锁啦！-->

 [1]: https://www.carlxu.cn/wp-content/uploads/2016/12/14830129921550.jpg
 [2]: https://assl.loovit.net/
 [3]: https://www.carlxu.cn/wp-content/uploads/2016/12/14829269245032.jpg
 [4]: https://www.carlxu.cn/wp-content/uploads/2016/12/14830129517637.jpg
 [5]: https://www.carlxu.cn/wp-content/uploads/2016/12/14830131375026.jpg
 [6]: https://www.carlxu.cn/wp-content/uploads/2016/12/14830126661765.jpg
 [7]: https://www.carlxu.cn/wp-content/uploads/2016/12/14830125685810.jpg
 [8]: https://www.carlxu.cn/wp-content/uploads/2016/12/14830124890895.jpg
 [9]: https://www.carlxu.cn/wp-content/uploads/2016/12/14830124443749.jpg
 [10]: https://www.carlxu.cn/wp-content/uploads/2016/12/14830138479212.jpg