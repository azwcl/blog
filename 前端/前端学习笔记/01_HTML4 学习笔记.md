@ -0,0 +1,971 @@
# HTML4 学习笔记

> 学习视频：[https://www.bilibili.com/video/BV1p84y1P7Z5](https://www.bilibili.com/video/BV1p84y1P7Z5/?p=2&spm_id_from=pageDriver&vd_source=d09f5eb0512a54fdebfa8d2cfc316137)

## 1. 前序知识

### 1.1. C/S 架构 与 B/S 架构

- C/S 架构：需要安装，偶尔更新，不跨平台，开发更具有针对性；

- B/S 架构：无需安装，无需更新，可跨平台，开发更具有通用性；

- > C : client 客户端；B：browser 浏览器；S：server 服务器

### 1.2. 浏览器相关知识

![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/17530184897291fb.png)

![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/1753018503832f5c.png)

### 1.3. 网页知识

1. 网址：我们在浏览器中输入的地址。
2. 网页：浏览器所呈现的每一个页面。
3. 网站：多个网页构成了一个网站。
4. 网页标准：

![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/17530185277bcb39.png)

## 2. HTML 简介

### 2.1. 什么是 HTML ？ 

全称：HyperText Markup Language（超文本标记语言）。

> 超文本：暂且简单理解为 “超级的文本”，和普通文本比，内容更丰富。

>  (是一种组织信息的方式，通过超链接将不同空间的文字、图片等各种信息组织在一起，能从当前阅读的内容，跳转到超链接指向的内容)

> 标 记：文本要变成超文本，就需要用到各种标记符号。

> 语 言：每一个标记的写法、读音、使用规则，组成了一个标记语言。

### 2.2. 一些联盟

1. IETF
   全称：Internet Engineering Task Force（国际互联网工程任务组），成立于1985年底，是一个权威的互联网技术标准化组织，主要负责互联网相关技术规范的研发和制定，当前绝大多数国际互联网
   技术标准均出自IETF。官网： https://www.ietf.org
2. W3C
   全称：World Wide Web Consortium（万维网联盟），创建于1994年，是目前Web技术领域，最具影响力的技术标准机构。共计发布了200多项技术标准和实施指南，对互联网技术的发展和应用起到
   了基础性和根本性的支撑作用，官网： https://www.w3.org
3. WHATWF
   全称：Web Hypertext Application Technology Working Group（网页超文本应用技术工作小组）成立于2004年，是一个以推动网络HTML5 标准为目的而成立的组织。由Opera、Mozilla基金会、苹果，等这些浏览器厂商组成。官网： https://whatwg.org/



### 2.3. HTMl 发展历史（了解）

![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/175301862193936f.png)



## 3. 准备工作

- 下载 Chrome 浏览器，使用其进行开发；



## 4. HTML 入门

### 4.1. HTML 初体验

1. 第一步：鼠标右键 => 新建 => 文本文档 => 输入以下内容，并保存。
2. 第二步：修改后缀为.html ，然后双击打开即可。
   这里的后缀名，使用.htm 也可以，但推荐使用更标准的.html 。

    ```html
    <marquee>尚硅谷，让天下没有难学的技术！</marquee>
    ```

3. 程序员写的叫 源代码，要交给浏览器进行渲染。

4. 借助浏览器看网页的 源代码，具体操作：
   在网页空白处：鼠标右键 ==> 查看网页源代码

### 4.2. HTMl 标签

1. 标签又称为元素，是 HTML 的基本组成元素；
2. 标签分为：双标签 与 单标签；
3. 标签名不区分大小写，但推荐小写；
4. 标签之间的关系：并列、嵌套；可以使用 `tab` 键进行缩进；

### 4.3. HTMl 标签属性

1. 用来给标签提供**附加信息**；

2. 可以写在：起始标签 或 单标签 中，形式如下：

   ![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/17530188134e1382.png)

3. 有些特殊属性，没有属性名，只有属性值，例如：

   ```html
   <input disabled> 
   ```

4. 注意点：

   1. 不同的标签，有不同的属性，也有一些通用的属性；（在任何标签内都能写）

   2. 属性名、属性值不能乱写，都是W3C规定好的；

   3. 属性名、属性值，都不区分大小写，但推荐小写；

   4. 双引号，也可以写成单引号，甚至不写都行，但还是推荐写双引号；

   5. 标签中不要出现同名属性，否则后写的会失效，例如：

      ```html
      <input type="text" type="password">
      ```

### 4.4. HTML 基本结构

1. 在网页中，如何查看某段结构的具体代码？ -- 点击鼠标右键，选择“检查”。

2. 【检查】 和 【查看网页源代码】的区别：
   【查看网页源代码】看到的是：程序员编写的源代码。
   【检查】看到的是：经过浏览器 “处理” 后的源代码。

   >  备注：日常开发中，【检查】用的最多。

3. 网页的 基本结构 如下：

   1. 想要呈现在网页中的内容写在 `body` 标签中；

   2. `head` 标签的内容不会出现在网页中；

   3. `head` 标签中的 `title` 标签可以指定网页的标题；

   4. ![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/175301904732321d.png)

   5. ```html
      <html>
        <head>
          <title>网页标题</title>
        </head>
        <body>
          ......
        </body>
      </html>
      ```

### 4.5. 安装 VS Code

- 推荐 vscode-icons 插件；
- 推荐：Live Server 插件；

### 4.6. 注释

1. 特点：注释被浏览器忽略，不会呈现在页面中，但是在源代码中仍然可以见到；

2. 作用：对代码进行解释和说明；

3. 写法：

   ```html
   <!-- 这是注释 -->
   ```

4. 注释不可嵌套；

### 4.7. HTML 文档声明

1. 作用：告诉浏览器当前网页的版本；

2. 写法：

   1. 旧写法：要依网页所用的HTML版本而定，写法有很多。https://www.w3.org/QA/2002/04/valid-dtd-list.html

   2. 新写法：一切都变得简单了！W3C 推荐使用 HTML 5 的写法。

      ```html
      <!DOCTYPE html>
      或
      <!DOCTYPE HTML>
      或
      <!doctype html>
      ```

   3. 注意：文档声明，必须要在网页的第一行，且在 `html` 标签的外侧；

### 4.8. HTML 字符编码

- 统一采用 UTF-8 编码；

- 为了让浏览器正确渲染，可以通过 `meta` 标签配合 `charset` 属性指定字符编码：

  ```html
  <head>
    <meta charset="UTF-8"/>
  </head>
  ```

### 4.9. HTML 设置语言

1. 主要作用：

   1. 让浏览器显示对应的翻译提示；
   2. 有利于搜索引擎的优化；

2. 具体写法：

   ```html
   <html lang="zh-CN">
   ```

3. 扩展知识

   ```txt
   1. 第一种写法（ 语言-国家/地区 ），例如：
     zh-CN ：中文-中国大陆（简体中文）
     zh-TW ：中文-中国台湾（繁体中文）
     zh ：中文
     en-US ：英语-美国
     en-GB ：英语-英国
   2. 第二种写法（ 语言—具体种类）已不推荐使用，例如：
     zh-Hans ：中文—简体
     zh-Hant ：中文—繁体
   3. w3school 参考资料: 
     https://www.w3school.com.cn/tags/html_ref_language_codes.asp
     https://www.w3school.com.cn/tags/html_ref_country_codes.asp
   4. w3c 官网说明：
     https://www.w3.org/International/articles/language-tags/
   ```

### 4.10. HTML 标准结构

```html
<!DOCTYPE html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <title>我是一个标题</title>
</head>

<body>
</body>

</html>
```

- 配置 VScode 的内置插件 emmet ，可以对生成结构的属性进行定制；
- 在存放代码的文件夹中，存放一个 favicon.ico 图片，可配置网站图标；



## 5. HTML 基础

### 5.1. 开发者文档

- W3C官网：www.w3c.org
- W3School：www.w3school.com.cn
- MDN: developer.mozilla.org

### 5.2. 排版标签

| 标签名 | 标签含义         | 单/双标签 |
| ------ | ---------------- | --------- |
| h1~h6  | 标题             | 双        |
| p      | 段落             | 双        |
| div    | 无含义，整体布局 | 双        |

1. `h1` 最好写一个，`h2~h6` 适当多写
2. `h1~h6` 不可互相嵌套；
3. `p` 标签很特殊！里面不能有这三个标签了；

### 5.3. 语义化标签

- 概念：用特定的标签，去表达特定的含义；

- 原则：标签的默认效果不重要，语义最重要；

- 举例：`h1` 标签，效果是文字很大，但是不重要；语义是网页主要内容，这个重要；

- 优势：

  - 代码结构清晰可读性强；

  - 有利于 `SEO`；

  - 方便设备解析（如屏幕阅读器、盲人阅读器等）

### 5.4. 块级元素与行内元素

1. 块级元素：独占一行（排版标签都是）
2. 行内元素：不独占一行（ `input` 等）
3. 使用原则：
   1. 块级元素内 可以写 行内元素 和 块级元素；
   2. 行内元素内，不可写 块级元素，可写 行内元素；
   3. 特殊规则：
      1. `h1~h6` 不能互相嵌套；
      2. `p` 中不要写块级元素；

### 5.5. 文本标签-常用

1. 用来包裹：词汇、短语等；
2. 通常写在排版标签内；
3. 排版标签更宏观，文本标签更微观；
4. 文本标签通常是行内元素；

| 标签名   | 标签语义                           | 单/双标签 |
| -------- | ---------------------------------- | --------- |
| `em`     | 着重阅读的内容                     | 双        |
| `strong` | 十分重要的内容（比 `em` 语气要强） | 双        |
| `span`   | 无语义，包裹短语的通用容器         | 双        |

> 生活例子：`div` 是大包装袋，`span` 是小包装袋；

### 5.6. 文本标签-不常用

| 标签名       | 标签语义                                                     | 单/双标签 |
| ------------ | ------------------------------------------------------------ | --------- |
| `cite`       | 作品标题（书籍、歌曲、电影、电视节目、绘画、雕塑）           | 双        |
| `dfn`        | 特殊术语、专属名词                                           | 双        |
| `del`        | 删除的文本                                                   | 双        |
| `ins`        | 插入的文本                                                   | 双        |
| `sub``sup`   | 上标与下标文本                                               | 双        |
| `code`       | 代码                                                         | 双        |
| `samp`       | 从正常的上下文中，将某些内容提取出来；例如：标识设备输出；   | 双        |
| `kbd`        | 键盘文本                                                     | 双        |
| `abbr`       | 缩写，最好配合 `title` 属性                                  | 双        |
| `bdo`        | 更改文本方向，要配合 `dir`属性，可选值：`ltr`（默认值），`rtl` | 双        |
| `var`        | 标记变量，可与 `code` 标签一起使用；                         | 双        |
| `small`      | 附属细则，例如：包括版权、法律文本；--很少用                 | 双        |
| `b`          | 摘要中的关键字、评论中的产品名称。--很少用                   | 双        |
| `i`          | 本意：人的思想活动，所说的话；现多用于：成仙字体图标         | 双        |
| `u`          | 与正常内容有反差文本，例如：错的单词、不合适的描述等。--很少使用 | 双        |
| `q`          | 短引用 --很少使用                                            | 双        |
| `blockquote` | 长引用 --很少使用                                            | 双        |
| `address`    | 地址信息                                                     | 双        |

> 备注：
>
> 1. 不常用的文本标签，编码不用纠结；
> 2. `blockquote` 和 `address` 是块级，其他都是行内元素；
> 3. 有些语义感不强的，很少使用：`small` `b` `u` `q` `blockquote`；
> 4. 记住上面语义强的即可：`h1~h6` `p` `div` `em` `strong` `span`；

### 5.7. 图片标签

#### 5.7.1. 基本使用

| 标签名 | 标签语义 | 常用属性                                                     | 单/双标签 |
| ------ | -------- | ------------------------------------------------------------ | --------- |
| `img`  | 图片     | `src`:图片路径`alt`:图片描述`width`:图片宽度`height`:图片高度 | 单        |

- 暂认为：行内元素；

- `alt`作用：

  - 搜索引擎通过属性，知道图片内容；

  - 当图片无法展示，部分浏览器会呈现 `alt` 属性值；

  - 盲人阅读器会朗读其值；

#### 5.7.2. 路径分类

- 相对路径
- 绝对路径

#### 5.7.3. 常见图片格式

1. `jpg`
   1. 概述：`jpg`或者 `jpeg`，有损压缩格式；
   2. 特点：支持的颜色丰富、占用空间较小、不支持透明背景、不支持动态图。
   3. 场景：对图片细节没有极高要求的场景
2. `png`
   1. 概述：无损的压缩格式；
   2. 特点：支持颜色丰富，占用空间略大，支持透明背景，不支持动态图；
   3. 场景：①想让图片有透明背景；②想更高质量的呈现图片；
3. `bmp`
   1. 概述：不进行压缩的一种格式，在最大程度上保留图片更多的细节；
   2. 特点：支持的颜色丰富、保留的细节更多、占用空间极大、不支持透明背景、不支持动态图。
   3. 场景：对图片细节要求极高的场景； 
4. `gif`
   1. 概述：仅支持 256 种颜色，色彩呈现不是很完整；
   2. 特点：支持的颜色较少、支持简单透明背景、支持动态图；
   3. 场景：网页中的动态图片；
5. `webp`
   1. 概述：谷歌推出的一种格式，专门用来在网页中呈现图片；
   2. 特点：具备上述几种格式的优点，但兼容性不太好，一旦使用务必要解决兼容性问题；
   3. 场景：网页中的各种图片
6. `base64`
   1. 本质：一串特殊的文本，要通过浏览器打开，传统看图应用通常无法打开。
   2. 原理：把图片进行 `base64` 编码，形成一串文本。
   3. 如何生成：靠一些工具或网站。
   4. 如何使用：直接作为 `img` 标签的 `src` 属性的值即可，并且不受文件位置的影响。
   5. 使用场景：一些较小的图片，或者需要和网页一起加载的图片。

### 5.8. 超链接

- 主要作用：当前页面进行跳转；
- 可实现：
  - 跳转到指定页面；
  - 跳转到指定文件；
  - 跳转到描点位置；
  - 唤起指定应用；

| 标签名 | 标签语义 | 常用属性                                                     | 单/双 |
| ------ | -------- | ------------------------------------------------------------ | ----- |
| `a`    | 超链接   | `href`:指定要跳转到的具体目标;<br />`target`：如何打开: `_self`本串口打开，`_blank`新窗口打开;<br />`id`： 元素唯一标识，可用来设置描点;<br />`name`：元素名字，可以写在 `a` 标签内，可设置锚点； | 双    |

#### 5.8.1. 跳转到页面

```html
<!-- 跳转其他网页 -->
<a href="https://www.jd.com/" target="_blank">去京东</a>
<!-- 跳转本地网页 -->
<a href="./10_HTML排版标签.html" target="_self">去看排版标签</a>
```

#### 5.8.2. 跳转到文件

```html
<!-- 浏览器能直接打开的文件 -->
<a href="./resource/自拍.jpg">看自拍</a>
<a href="./resource/小电影.mp4">看小电影</a>
<a href="./resource/小姐姐.gif">看小姐姐</a>
<a href="./resource/如何一夜暴富.pdf">点我一夜暴富</a>
<!-- 浏览器不能打开的文件，会自动触发下载 -->
<a href="./resource/内部资源.zip">内部资源</a>
<!-- 强制触发下载 -->
<a href="./resource/小电影.mp4" download="电影片段.mp4">下载电影</a>
```

> 1. 若浏览器无法打开，则会引导用户下载；
> 2. 若想要强制触发下载，使用 `download` 属性；值为下载文件的名称；

#### 5.8.3. 跳转到锚点

- 什么是锚点？-- 网页中的一个标记点；

  ```html
  <!-- 第一种方式：a标签配合name属性 -->
  <a name="test1"></a>
  <!-- 第二种方式：其他标签配合id属性 -->
  <h2 id="test2">我是一个位置</h2>
  
  注意：
  1. 具有 href 属性的 a 标签是超链接，具有 name 属性的 a 标签是锚点。
  2. name 和id 都是区分大小写的，且id 最好别是数字开头。
  
  
  <!-- 跳转到test1锚点-->
  <a href="#test1">去test1锚点</a>
  <!-- 跳到本页面顶部 -->
  <a href="#">回到顶部</a>
  <!-- 跳转到其他页面锚点 -->
  <a href="demo.html#test1">去demo.html页面的test1锚点</a>
  <!-- 刷新本页面 -->
  <a href="">刷新本页面</a>
  <!-- 执行一段js,如果还不知道执行什么，可以留空，javascript:; -->
  <a href="javascript:alert(1);">点我弹窗</a>
  ```

#### 5.8.4. 唤起指定应用

```html
<!-- 唤起设备拨号 -->
<a href="tel:10010">电话联系</a>
<!-- 唤起设备发送邮件 -->
<a href="mailto:10010@qq.com">邮件联系</a>
<!-- 唤起设备发送短信 -->
<a href="sms:10086">短信联系</a>
```

### 5.9. 列表

#### 5.9.1. 有序列表

```html
<h2>要把大象放冰箱总共分几步</h2>
<ol>
  <li>把冰箱门打开</li>
  <li>把大象放进去</li>
  <li>把冰箱门关上</li>
</ol>
```

![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/1753057031c77b82.png)

#### 5.9.2. 无序列表

```html
<h2>我想去的几个城市</h2>
<ul>
  <li>成都</li>
  <li>上海</li>
  <li>西安</li>
  <li>武汉</li>
</ul>
```

#### 5.9.3. 嵌套列表

```html
<h2>我想去的几个城市</h2>
<ul>
  <li>成都</li>
  <li>
    <span>上海</span>
    <ul>
      <li>外滩</li>
      <li>杜莎夫人蜡像馆</li>
      <li>
        <a href="https://www.opg.cn/">东方明珠</a>
      </li>
      <li>迪士尼乐园</li>
    </ul>
  </li>
  <li>西安</li>
  <li>武汉</li>
</ul>
```

注意：`li` 标签最好写在 `ui` 或者 `ol` 中，不可单独使用；

#### 5.9.4. 自定义列表

1. 概念：就是一个包含术语名称和术语描述的列表；

2. 一个 `dl` 就是一个自定义列表；一个 `dt` 就是一个术语名称；一个 `dd` 就是术语描述；

```html
<h2>如何高效的学习？</h2>
<dl>
  <dt>做好笔记</dt>
  <dd>笔记是我们以后复习的一个抓手</dd>
  <dd>笔记可以是电子版，也可以是纸质版</dd>
  <dt>多加练习</dt>
  <dd>只有敲出来的代码，才是自己的</dd>
  <dt>别怕出错</dt>
  <dd>错很正常，改正后并记住，就是经验</dd>
</dl>
```

![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/17530572633e70b1.png)

### 5.10. 表格

#### 5.10.1. 基本结构

1. 一个完整的表格由：表格标题、表格头部、表格主题、表格脚注 四部分构成；

   ![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/17530573262dd61d.png)

2. 表格涉及到的标签

   1. `table` 表格；
   2. `caption` 表格标题；
   3. `thead` 表格头部；
   4. `tbody` 表格主题；
   5. `tfoot` 表格注脚；
   6. `tr` 每一行；
   7. `th`、`td` 每一个单元格（表头用：`th`，表格主题表格脚注用：`td` ）；

   ![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/1753057425c998cb.png)

   ![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/1753057434a04a2a.png)

   ![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/175305744336ccb5.png)

3. 具体编码

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
   </head>
   <body>
       <table border="1px">
           <!-- 表格标题 -->
           <caption>学生信息</caption>
           <thead>
               <tr>
                   <th>姓名</th>
                   <th>性别</th>
                   <th>年龄</th>
                   <th>民族</th>
                   <th>政治面貌</th>
               </tr>
               <tbody>
                   <tr>
                       <td>张三</td>
                       <td>男</td>
                       <td>18</td>
                       <td>汉族</td>
                       <td>团员</td>
                   </tr>
                   <tr>
                       <td>李四</td>
                       <td>男</td>
                       <td>20</td>
                       <td>满族</td>
                       <td>群众</td>
                   </tr>
               </tbody>
               <tfoot>
                   <tr>
                       <td></td>
                       <td></td>
                       <td></td>
                       <td colspan="2">共计：2人</td>
                   </tr>
               </tfoot>
           </thead>
       </table>
   </body>
   </html>
   ```

#### 5.10.2. 常用属性

| 标签名  | 标签语义   | 常用属性                                                     | 单/双 标签 |
| ------- | ---------- | ------------------------------------------------------------ | ---------- |
| `table` | 表格       | `width`: 设置表格宽度；<br />`height`：设置表格最小高度；最终高度可能会比设置值大；<br />`border`：设置表格边框宽度；<br />`cellspacing`：设置单元格之间的间距； | 双         |
| `thead` | 表格头部   | `height`：表格头部高度；<br />`align`：单元格的水平对齐方式；<br />-    `left`：左对齐；<br />-    `center`：中间对齐；<br />-    `right`：右对齐；<br />`valign`：单元格垂直对齐方式；<br />-    `top`：顶部对齐；<br />-    `middle`：中间对齐；<br />-    `bottom`：底部对齐； | 双         |
| `tbody` | 表格主体   | 常用属性与 `thead`相同                                       | 双         |
| `tr`    | 行         | 常用属性与 `thead`相同                                       | 双         |
| `tfoot` | 表格脚注   | 常用属性与 `thead`相同                                       | 双         |
| `td`    | 普通单元格 | `width`：单元格宽度，同列所有单元格均受影响；<br />`height`：单元格高度，同行所有单元格均受影响；<br />`align`：水平对齐方式；<br />`valign`：垂直对齐方式；<br />`rowspan`：指定要跨行数；<br />`colspan`：指定要跨列数； | 双         |
| `th`    | 表头单元格 | 常用属性与 `td` 相同                                         | 双         |

注意点：

1. `table` 元素的 `border` 属性可以控制表格边框，但 `border` 值的大小，并不控制单元格边框的宽度；
2. 默认情况，每列的宽度，得看这一列单元格最长的那个文字；
3. 给某个 `th` 或 `td` 设置了宽度 / 高度之后，他们所在的那一列/行 宽度/高度就确定了；

### 5.11. 常用标签补充

1. `br` 换行标签，单标签；
2. `hr` 分隔标签，单标签；
3. `pre` 按照原文显示，双标签；

> 注意：
>
> 1. 不要用 `br` 标签来增加文本的行间隔，应用 `p` 元素，或 CSS；
> 2. `hr` 语义是分隔，不想要语义，只想画水平线的画，应该用 CSS；

### 5.12. 表单

- 一个包含交互的区域，用来收集用户提供的数据；

#### 5.12.1. 基本结构

| 标签名   | 标签语义 | 常用属性                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| `form`   | 表单     | `action`：用于指定表单的递交地址；<br />`target`：用于控制表单递交后，如何打开页面；<br />-    `_self`：本窗口打开<br />-    `_blank`：新窗口打开<br />`method`：控制表单的提交方式 |
| `input`  | 输入框   | `type`：类型`name`：提交数据的名字                           |
| `button` | 按钮     | 暂不涉及                                                     |

```html
<form action="https://www.baidu.com/s" target="_blank" method="get">
  <input type="text" name="wd">
  <button>去百度搜索</button>
</form>
```

#### 5.12.2. 常用表单控件

1. 文本输入框

   ```html
   <input type="text">
   ```

   - 常用属性：
     - `name` : 数据的名称；
     - `value` : 输入框的默认输入值；
     - `maxlength` : 输入框最大可输入长度；

2. 密码输入框

   ```html
   <input type="password">
   ```

   - 常用属性同文本输入框

3. 单选框

   ```html
   <input type="radio" name="sex" value="female">女
   <input type="radio" name="sex" value="male">男
   ```

   - 常用属性：
     - `name`：数据的名称，如果要实现单选效果，多个 `radio` 的 `name` 须一致；
     - `value`：提交的数据值；
     - `checked`：单选按钮默认选中；

4. 复选框

   ```html
   <input type="checkbox" name="hobby" value="smoke">抽烟
   <input type="checkbox" name="hobby" value="drink">喝酒
   <input type="checkbox" name="hobby" value="perm">烫头
   ```

   - 常用属性：
     - 同单选框；

5. 隐藏域

   ```html
   <input type="hidden" name="tag" value="100">
   ```

   - 常用属性有：`name` 和 `value` ；其作用，提交数据的时候，携带一些固定数据；

6. 提交按钮

   ```html
   <input type="submit" value="点我提交表单">
   <button>点我提交表单</button>
   ```

   - 注意：
     - `button` 标签 `type` 属性的默认值是 `submit`；
     - `button` 不要指定 `name` 属性；
     - `input` 标签编写的按钮，使用 `value`属性指定按钮文字；

7. 重置按钮

   ```html
   <input type="reset" value="点击重置">
   <button type="reset">点我重置</button>
   ```

   - 注意：
     - 同提交按钮；

8. 普通按钮

   ```html
   <input type="button" value="普通按钮">
   <button type="button">普通按钮</button>
   ```

9. 文本域

   ```html
   <textarea name="msg" rows="22" cols="2">文本域</textarea>
   ```

   - 常用属性：
     - `rows` 属性：显示行数；影响文本域的高度；
     - `cols` 属性：显示列数；影响文本域的宽度；
     - 不可编写 `type` 属性，其他属性与普通文本输入框一致；

10. 下拉框

    ```html
    <select name="from">
      <option value="黑龙江">黑龙江</option>
      <option value="辽宁">辽宁</option>
    </select>
    ```

    - 常用属性及注意点：
      - `name` ：数据的名称；
      - `option` 标签设置 `value` 属性，如果没有 `value`属性，则会提交 `option` 中间的文字；如果设置，则提交 `value` 的值；
      - `option` 设置了 `selected` 的属性，标识默认选中；

#### 5.12.3. 禁用表单控件

- 给表单控件的标签加上 `disabled` 可以禁用表单控件；
- `input` 、`textarea` 、 `button` 、`select` 、`option` 都可以设置 `disabled` 的属性；

#### 5.12.4. `label` 标签

- 该标签可与表单控件相关联，关联之后点击文字，与之对应的表单控件就会获取焦点；

- 两种关联方式：

  - `label` 的 `for` 属性的值等于表单控件的 `id` ；

  - 将表单控件套在 `label` 标签之中；

#### 5.12.5. `fieldset` 和 `legend` 使用

- `fieldset` 可以为表单控件分组；
- `legend` 为分组的标题；

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <form action="">
        <fieldset>
            <legend>主要信息</legend>
            <label for="zhanghu">账户：</label>
            <input id="zhanghu" type="text" name="account" maxlength="10"><br>
            <label>
                密码：
                <input id="mima" type="password" name="pwd" maxlength="6">
            </label>
            <br>
            性别：
            <input type="radio" name="gender" value="male" id="nan">
            <label for="nan">男</label>
            <label>
                <input type="radio" name="gender" value="female" id="nv">女
            </label>
        </fieldset>
    </form>
</body>

</html>
```

![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/17530582449c318e.png)

### 5.13. 框架标签

| 标签名   | 功能与语义                 | 属性                                                         |
| -------- | -------------------------- | ------------------------------------------------------------ |
| `iframe` | 框架（在网页中嵌入其他文件 | `name`：框架名字，可以与 `target`配合；<br />`width` 和 `height`：宽高；<br />`frameborder`：是否显示边框；0/1 |

- 实际应用：

  - 网页中嵌入广告；

  - 与 超链接或表单的 `target` 配合，展示不同内容；

    ```html
    <!DOCTYPE html>
    <html lang="en">
    
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    
    <body>
        <a href="https://www.bilibili.com" target="tt">点我看b站</a>
        <iframe name="tt" ></iframe>
    </body>
    
    </html>
    ```

### 5.14. 字符实体

- HTML 中我可以用特殊的形式表示某个符号；这就是 HTML 实体；因为对于 `<` 这种，我们会希望浏览器正确显示，所以必须要在 HTML 源码中插入字符实体；

- HTML 实体参考：

  - https://html.spec.whatwg.org/multipage/named-characters.html#named-character-references

  - https://www.runoob.com/html/html-entities.html

    ![img](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/1753058334420345.png)

### 5.15. 全局属性

| 属性名         | 含义                                                         |
| -------------- | ------------------------------------------------------------ |
| `id`           | 标签的唯一标识，不可重复；                                   |
| `class`        | 标签指定类名                                                 |
| `style`        | 标签设置 `css` 样式                                          |
| `dir`          | 内容的方向；值：`ltr` 和 `rtl`                               |
| `title`        | 标签设置一个文字提醒                                         |
| `lang`         | 给标签指定语言；                                             |
| 完整的全局属性 | https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes |

### 5.16. `meta` 元信息

1. 配置字符编码

   ```html
   <meta charset="utf-8">
   ```

2. 针对 ie 浏览器的兼容性配置

   ```html
   <meta http-equiv="X-UA-Compatible" content="IE=edge">
   ```

3. 针对移动端配置

   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   ```

4. 配置网页关键字

   ```html
   <meta name="keywords" content="8-12个以英文逗号隔开的单词/词语">
   ```

5. 配置网页描述信息

   ```html
   <meta name="description" content="80字以内的一段话，与网站内容相关">
   ```

6. 针对搜索引擎爬虫配置

   ```html
   <meta name="robots" content="此处可选值见下表">
   ```

   | 值          | 描述                     |
   | ----------- | ------------------------ |
   | `inde`      | 允许索引                 |
   | `noindex`   | 不允许索引               |
   | `follow`    | 允许跟随此页面上链接；   |
   | `nofollow`  | 不允许跟随页面上链接     |
   | `all`       | 等价 `index, follow`     |
   | `none`      | 等价 `noindex，nofollow` |
   | `noarchive` | 要求不缓存页面内容       |
   | `nocache`   | `noarchive`替代名称      |

7. 配置网页作者

   ```html
   <meta name="author" content="tony">
   ```

8. 配置网页生成工具

   ```html
   <meta name="generator" content="Visual Studio Code">  
   ```

9. 配置定义网页版权信息

   ```html
   <meta name="copyright" content="2023-2027©版权所有">
   ```

10. 配置网页自动刷新

    ```html
    10 秒后自动重定向到 www.baidu.com
    <meta http-equiv="refresh" content="10;url=http://www.baidu.com">
    ```

11. 参考完整的网页元信息：https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meta

## 6. 总结

![总结图片](https://azwcl-blog.oss-cn-shanghai.aliyuncs.com/picgo/2025/07/17530586519d21ff.png)
