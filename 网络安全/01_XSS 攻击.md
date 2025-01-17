# XSS攻击

### 一、XSS漏洞
XSS漏洞很常见，在很多网站中都存在着

首先：
引用维基百科的一句话：
> 跨站脚本（英语：Cross-site scripting，通常简称为：XSS）是一种网站应用程序的安全漏洞攻击，是代码注入的一种。它允许恶意用户将代码注入到网页上，其他用户在观看网页时就会受到影响。这类攻击通常包含了HTML以及用户端脚本语言。
> XSS攻击通常指的是通过利用网页开发时留下的漏洞，通过巧妙的方法注入恶意指令代码到网页，使用户加载并执行攻击者恶意制造的网页程序。这些恶意网页程序通常是JavaScript，但实际上也可以包括Java，VBScript，ActiveX，Flash或者甚至是普通的HTML。攻击成功后，攻击者可能得到更高的权限（如执行一些操作）、私密网页内容、会话和cookie等各种内容。

### 二、XSS介绍

可能听到上面引用的话，觉得XSS攻击狠高大上，其实XSS攻击很简单，是一种嵌入了代码中的攻击，嵌入在前端的js中，然后浏览器加载这段js，从而达到目的。
有人可能说，嵌入到别人网页的js中，怎么可能做到？

再说一个实例，富文本默认不过滤XSS漏洞，markdown也有XSS漏洞，XSS漏洞广泛存在，在编辑富文本的时候，你就可以修改文中一些东西，从而植入js代码，从而达到一些很美妙的目的，执行一系列操作。

XSS分成几个类别：
- 存储型XSS
- 反射型XSS
- DOM型XSS

分别介绍一下：
1. 存储型XSS攻击：是攻击者将恶意的代码提交到目标网站的数据库中，用户打开目标网站，网站服务器提取代码，放在HTML中返回给浏览器，用户浏览器接收到响应后解析执行，其中这一恶意代码也会被执行。
2. 反射型XSS攻击：攻击者构造出来一段特殊的URL，其中这段URL中包含着恶意代码，用户打开恶意代码的时候，执行恶意代码。不过这个和上面的有很大区别，这个要诱导用户自己点击，而上面的加载就行了，因为这个URL需要用户主动打开才能生效。
3. DOM型XSS攻击：攻击者构造特殊URL，用户浏览器接收到响应解释执行后，前端JS去除URL中而已代码进行执行。这个和上面的区别是，这个DOM型属于浏览器端完成，属于前端的漏洞，上面的两种属于服务器端的安全漏洞。这个DOM型XSS攻击其实也属于反射型的一种，但是DOM型和反射型有一个区别点在于，反射型需要与后台交互，DOM型缺不需要。例如现在有个网页是:`127.0.0.1/demo.html`，现在攻击者将其URL中嵌入：`127.0.0.1/demo.html?demo=<script>alert('Hello XSS')</script>`，这样子便会出现一个弹窗。这其实就是DOM型XSS攻击的最简单的例子。

### 三、我的实地攻击（2019.6.29补）
我发现很多的网站，特别是中小型网站都有XSS漏洞的缺点。
其中该攻击，是针对我学校的网站攻击的，利用的是存储型XSS
步奏：
1. 在富文本编译器中植入相关js代码，获取用户cookie
2. 将获取的cookie发送到我的服务器中，进行存储，存储在数据库中
3. 伪造cookie进行登录，期间甚至获取到管理员的cookie。

附图：
![](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2024/11/1730729725e89c1c.jpeg)

### 四、预防XSS漏洞
1. 转义
对代码中特殊的字符进行相关转义，保证其不会再代码中运行
对：`& < > " ' / `进行相关转义，保证不会运行该js

2. 过滤
过滤相关属性及事件，例如：`onload`事件，`onerror`事件等等，像这些过滤掉，特别是富文本编译器中所有事件都不应该存在，因为不需要，所以应该过滤了所有的事件。以此达到防范XSS漏洞的目的。

3. 预防前端执行
将网页拥有相关XSS漏洞的地方进行改造，以纯前端方式渲染。
先渲染网页的静态HTML部分，此部分不包括任何数据，其词，执行HTML中JS部分，再通过异步方法获取数据，将其加载在页面上，明确告诉浏览器是文本，亦或是属性，还是别的，这样便不会被轻易欺骗

4. CSP （Content Security Policy）（我暂时未使用过该方法，网上的一种特别有效的解决方法，技术小白默默流泪）
> 禁止加载外域代码，防止复杂的攻击逻辑。
> 禁止外域提交，网站被攻击后，用户的数据不会泄露到外域。
> 禁止内联脚本执行（规则较严格，目前发现 GitHub 使用）。
> 禁止未授权的脚本执行（新特性，Google Map 移动版在使用）。

5. 总结
存储型以及反射型的XSS漏洞应有后端开发人员进行防范
DOM型由于不与服务器端进行交互，故应由前端开发人员进行防范
好的网站进行过滤XSS的时候，应当前后端相互配合，进行防范