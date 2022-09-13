# 实验原理


&emsp;&emsp;

!!! info "说明 :sparkles:"
&emsp;&emsp;P代表明文，Pi代码第i个明文分组，C代表密文，Ci代表第i个密文分组，K代表密钥，IV代表初始化向量。

## 1. AES密码算法

&emsp;&emsp;。

&emsp;&emsp;中间人攻击时发生在两个设备之间的流量被截获的情况下。当一台计算机向另外一台计算机发送数据时，数据会在多个设备之间传输，例如路由器。这些设备如果被攻击，就可以被用来实施中间人攻击。如下图所示：
<center><img src="../assets/2-1.png" width = 500></center>
<center>图2-1 中间人攻击的原理</center>

&emsp;&emsp;中间人攻击的基本问题是通信双方无法确定这个公钥是否属于对方，如果能够提供一个机制把公钥和所有者的身份绑定在一起，那么就可以解决这个问题。公钥基础设施（PKI）就是解决此问题的一个方案。

## 2. 填充方式

### 2.1 NoPadding：不填充，明文的字节长度只能是16的整数倍，一般不适用。
&emsp;&emsp;示例1

### 2.2 Zeros：补0，如果原数据字节长度恰好是16的倍数，也要补充多16个0；
&emsp;&emsp;示例1

&emsp;&emsp; 示例2

!!! info "攻击点 :sparkles:"
&emsp;&emsp;

### 2.2 ISO10126：最后一个字节是填充的字节数（包括最后一个字节自己），其他全部填随机数。
&emsp;&emsp;示例1

&emsp;&emsp; 示例2

!!! info "攻击点 :sparkles:"
&emsp;&emsp;

### 2.3 PKCS5(PKCS7)：最后一组缺几个字节就填充几

&emsp;&emsp;示例1

&emsp;&emsp; 示例2

!!! info "攻击点 :sparkles:"
&emsp;&emsp;

## 3. 工作模式

&emsp;&emsp; 我们通过下图看以下Https访问web时的证书应用场景，Https服务器通过访问CA申请并获得一个证书，管理员通过这个证书来验证这个证书就可以了。

### 3.1 【了解】电码本模式（Electronic Codebook Book,简称ECB）：将明文按16个字节分组，每组分别加密后再拼接在一起就是加密后的明文。其缺点是如果分组的明文相同，那么对应的密文也将相同。因此常用于比较短的数据加密，比如密钥的加密。

<center><img src="../assets/3-1.png" width = 800></center>

!!! info "说明 :sparkles:"
&emsp;&emsp;最后一个分组：是否需要填充：是
&emsp;&emsp;是否需要初始化向量：否

### 3.2 【本次实验需要完成】密文分组链接模式（Cipher Block Chaining, 简称CBC）：每一组明文先与初始化向量或者上一组的密文进行异或，得到的结果再与密钥进行加密。具体如下图所示。

<center><img src="../assets/3-2.png" width = 800></center>

!!! info "说明 :sparkles:"
&emsp;&emsp;最后一个分组是否需要填充：是
&emsp;&emsp;是否需要初始化向量：是

### 3.3 【了解】密文反馈模式（Cipher FeedBack, 简称CFB）：在上面两个工作模式ECB和CBC中，整个数据分组需要在接收完之后才能进行加密。但是在一些网络应用中，需要即刻把一个终端输入的字符传给主机。这样上面的两种工作模式就不能满足。在CFB模式中，数据可以在比分组（8bytes）小的单元里进行加密。其工作方式类似流密码。
&emsp;&emsp;CFB模式中，假设传输的最小单元是s（下图以8bits为例）位，分组大小为b位（AES分组的大小是128bits）。首先将初始化向量IV放到b位的移位寄存器中，加密函数输出最左边的s位，与明文分片P1进行异或，得到的密文C1并发送，然后把移位寄存器左移s位，把C1填入寄存器最右边的s位开始第二个明文分片的加密。具体如下图所示。

<center><img src="../assets/3-3.png" width = 800></center>

!!! info "说明 :sparkles:"
&emsp;&emsp;最后一个分组是否需要填充：否
&emsp;&emsp;是否需要初始化向量：是

### 3.4 【了解】输出反馈模式（Output FeedBack, 简称OFB）：OFB模式的结构跟上面CFB的模式很相似，不同的是它用加密函数的输出来填充移位寄存器，而CFB是用密文单元来填充移位寄存器。而且它是对这个分组来运算的。

<center><img src="../assets/3-4.png" width = 800></center>

!!! info "说明 :sparkles:"
&emsp;&emsp;最后一个分组是否需要填充：否
&emsp;&emsp;是否需要初始化向量：是


### 3.5 【可深入了解】计数器模式（Counter, 简称CTR）：计数器模式使用与明文文组规模相同的长度，第一个明文分组与加密后的初始的计数器进行异或，后面随着消息块的增加计数器的值加1。

<center><img src="../assets/3-5.png" width = 800></center>

!!! info "说明 :sparkles:"
&emsp;&emsp;最后一个分组是否需要填充：否
&emsp;&emsp;是否需要初始化向量：是

### 3.6 其他几种工作模式

#### 3.6.1 CCM模式：为了保证消息的可靠性与完整性，根据密文分组链将计数器模式与消息认证码（MAC）结合。

#### 3.6.2 CCM模式：