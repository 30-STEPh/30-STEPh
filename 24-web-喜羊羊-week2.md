首先得我的狡辩一下为啥交的这么晚，因为上回我的md里面的图片采用相对路径的方式去显示，效果并不好，所以我跑去研究图床，一步步按照网上的教程去做，一直上传失败，不断地调整设置，弄了4个多小时，不见效果，已经是给我气笑了，然后我破罐子破摔式的重启了机器，

然后，它，他妈的传上去了！

研究了一下，应该是这玩意的锅，我习惯用这个去打开steam和github

![image-20250324012001486](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012001555.png)

这下问题解决了，唉，菜是原罪

## 拓展的配置--hackbar

首先鼠鼠要看一下hackbar是怎么用的，因为鼠鼠更倾向于使用burpsuit，下载两个免费版本的hackbar,一个无法使用就切另一个

![在这里插入图片描述](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012154214.png)

csdn给出了详细的介绍

SQL：提供三种数据库的sql查询语句，以及一些方便联合查询的语句
XSS：提供xss攻击语句
string.fromcharcode()：将根据UNICODE 值来输出xss语句
html charactor ： 将XSS语句转化为HTML字符实体（以&开头）
alert(xss) statement : 构建一条xss测试语句，弹出一个框内容为xss，相当于alert(‘xss’);
Encryption：对所选字符进行加密，提供了MD5，SHA-1，SHA-256，ROT13等加密方式
Encoding：对所选字符进行编码解码，提供了Base64 Encode,Base64 Decode,URLencode,URLdecode,
HEX encoding, HEX decoding等方式
Other：
addslashes：在每个双引号前加反斜杠
stripslashes：除去所选字符中的反斜杠
strip space：除去所选字符中的空格
reverse：将所选字符倒序排列
usefull strings：提供了一些特殊的数值如圆周率PI,斐波那契数列等，其中buffer overflow 可以输入一定长度的字符造成缓存溢出攻击
大致是这样，以后会细细探究。

## [LitCTF 2023]Follow me and hack me--burpsuit

![image-20250318173723058](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012200368.png)

神经。。。。。。。。。。。。

![image-20250318184637559](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012205470.png)

尝试向里面传参数， 在URL中使用?符号将参数附加到URL末尾，多个参数之间使用&符号分隔。

使用POST提交方法和GET类似，将GET改为POST，此时记得添加Content-Type: application/x-www-form-urlencoded

![image-20250318184735320](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012209739.png)

![image-20250318185055295](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012214290.png)

## [SWPUCTF 2021 新生赛]Do_you_know_http

![image-20250319214553466](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012219002.png)

![image-20250319215015202](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012221966.png)

![image-20250319215631798](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012228667.png)

修改user agent为WLLM   execute一下

![image-20250319220536064](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012225307.png)

不难发现，我们要伪造一个用WLLM浏览器的进入方式，即修改user agent,得到一个a.php的文件，这个文件只能在本地打开，我们要在<font color='green'>本地回环地址</font>中打开，得到答案。

## [LitCTF 2023]就当无事发生

![image-20250323153416596](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012232690.png)

进入了一个网站，不明白这道题想干嘛。

进入他的github主页也没找到上面的flag文件，但是找到了不少index文件，也看到了这位大佬的学习与工作过程。



## [第五空间 2021]WebFTP

![image-20250324021010173](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324021010234.png)

这是一个登录的界面，我们随意的输入用户名和密码试一试。

账户不存在或密码有误，这和那个ctfhub的技能书里面有一道题非常非常像，用bp抓包试一下吧。

![image-20250324021405608](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324021405749.png)

突然想起来，这个是git泄露的题













## 一些知识的补充

### 本地回环地址

回环地址并非只有一个，所有127开头的都是回环地址。

而***<font color='red'>本地</font>回环地址***127.0.0.1指的是本机地址，不会跟着网络情况的变化而变化。它代表设备的本地虚拟接口，所以默认被看作是永远不会宕掉的接口。(实际上：127.0.0.1 —> 127.255.255.254（去掉0和255） 的范围都是本地回环地址)

**它的作用是**计算机以回环地址发送的消息，并不会由链路层送走，而是被本机网络层捕获。用处只有一个，就是自己发给自己，自娱自乐。

### **X-Forwarded-For**（**XFF**）

**X-Forwarded-For**（**XFF**）是用来识别通过[HTTP](https://baike.baidu.com/item/HTTP/0?fromModule=lemma_inlink)[代理](https://baike.baidu.com/item/代理/0?fromModule=lemma_inlink)或[负载均衡](https://baike.baidu.com/item/负载均衡/0?fromModule=lemma_inlink)方式连接到[Web服务器](https://baike.baidu.com/item/Web服务器/0?fromModule=lemma_inlink)的客户端最原始的[***IP地址***](https://baike.baidu.com/item/IP地址/0?fromModule=lemma_inlink)的<font color='red'>HTTP请求头字段。</font>

#### 用法

一般格式如下:

**<font color='red'>X-Forwarded-For: client1, proxy1, proxy2, proxy3</font>**

***其中的值通过一个 逗号+空格 把多个IP地址区分开***

最左边(client1)是**最原始客户端的IP地址**, 代理服务器每成功收到一个请求，就把**请求来源IP地址**添加到右边。 

在上面这个例子中，这个请求成功通过了三台代理服务器：proxy1, proxy2 及 proxy3。请求由client1发出，到达了proxy3(proxy3可能是请求的终点)。

请求刚从client1中发出时，XFF是空的，请求被发往proxy1；通过proxy1的时候，client1被添加到XFF中，之后请求被发往proxy2;通过proxy2的时候，proxy1被添加到XFF中，之后请求被发往proxy3；通过proxy3时，proxy2被添加到XFF中，之后请求的的去向不明，如果proxy3不是请求终点，请求会被继续转发。

鉴于伪造这一字段非常容易，应该谨慎使用X-Forwarded-For字段。正常情况下XFF中最后一个IP地址是最后一个代理服务器的IP地址, 这通常是一个比较可靠的信息来源。

### Index

我们先来理解下 Git 工作区、暂存区和版本库概念：

- **工作区：**就是你在电脑里能看到的目录。
- **暂存区：**英文叫 stage 或 index。一般存放在 **.git** 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
- **版本库：**工作区有一个隐藏目录 **.git**，这个不算工作区，而是 Git 的版本库。

![img](https://raw.githubusercontent.com/30-STEPh/photos/main/20250324012236318.jpg)

### git泄露

#### git是什么

**Git**是一个开源的分布式版本控制系统，它能够高效地处理从小到大的项目。Git的核心功能是版本控制，它允许你跟踪文件的变化，保存不同版本的文件，并且在需要的时候可以回退到任何一个历史版本。这在软件开发中尤其有用，因为它允许多人协作开发同一个项目，同时保持各自的开发进度和变更记录。

**本地仓库**：是在开发人员自己电脑上的Git仓库
**远程仓库**：是在远程服务器上的Git仓库

Clone：克隆，就是将远程仓库复制到本地
Push：推送，就是将本地仓库代码上传到远程仓库
Pull：拉取，就是将远程仓库代码下载到本地仓库