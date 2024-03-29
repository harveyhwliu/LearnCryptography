## 一、 密码学基本概念

### 1. 引子 - 最早的密码学
#### Caesar密码(凯撒密码)
&emsp;&emsp;它是一种代换密码,凯撒密码作为一种最为古老的`对称加密体制`，在古罗马的时候都已经很流行，他的基本思想是： `通过把字母移动一定的位数来实现加密和解密`。明文中的所有字母都在字母表上向后（或向前）按照一个固定数目进行偏移后被替换成密文。`位数就是凯撒密码加密和解密的密钥`。举例:<br/>
       
   - 举例:<br/> 
       - 明文： meet me after the toga party <br/>
       - 密文： PHHW PH DIWHU WKH WRJD SDUWB <br/>
       - 加密算法: Ci = E(Pi) = Pi + 3,移位密码的k = 3 <br/>
   
   - 密码学中，`明文，密文， 密钥，加密算法和解密算法`称为五元组.<br/>
      - 明文： 原始信息<br/>
      - 密文： 加密后的信息<br/>
      - 密钥： 加密解密时使用的参数<br/>
      - 密钥空间：所有密钥的可能取值空间<br/>
      - 加密算法： 将明文转化为密文的算法<br/>
      - 解密算法： 加密算法的逆<br/>
      
&emsp;&emsp;那么，Caesar密码是否安全？答案是：肯定不安全，因为Caesar密码的密钥空间太小了，Caesar移位密码只有25种密匙，最多就是将这25种可能性挨个检测一下可以了，这就是我们所说的暴力破解法。只需简单地统计字频就可以破译。现今又叫“移位密码”，只不过移动的位数不一定是3位而已。<br/>
#### 替换密码(substitution cipher)
&emsp;&emsp;从caesar密码可知，密钥空间小肯定不安全，那如果密钥空间大就安全么？<br/>
   - 我们假设有一个密码明文/密文的查找表，如下:  <br/> 
       - 明文： abcdefghijklmnopqrstuvwxyz <br/>
       - 密文： FLGIJKMNUYDSOPQEBRTVWHXZAC <br/>
       - 加密算法: 将明文按照上面的`密码查找表`找到对应的密文<br/>
       - 举例： 明文 caesar cipher 经过替换密码后的 密文是 GFJTFR GUENJW， 比如明文e 对应的密文是J
       - 密钥空间: 26！<br/>
       
&emsp;&emsp;从上面的例子可知，密钥空间已经足够大了为26！但是上面的加密方式并不安全。上面加密算法的一个重要的特点是：`明文中相同字母对应的密文是一样的`，可以`采用字母频率攻击`破解。<br/>
&emsp;&emsp;字母频率，指的是各个字母在文本材料中出现的频率。常被应用于密码学，`尤其是可破解古典密码的频率分析`。在英语中最常见的字母是e（13%），其次是T(9)%(字母频率攻击通常会考虑最常用的首写字母，连词字母等等信息)。摩斯电码中越常用的字母，其编码符号就越短；数据压缩技术中也有相似的方法，如霍夫曼编码就是按来源符号出现的机率大小去编码。<br/>
 #### Kerckhoffs原理(科克霍夫原则)
&emsp;&emsp;由奥古斯特·柯克霍夫在19世纪提出：即使密码系统的任何细节已为人悉知，只要密匙（key，又称金钥或密钥）未泄漏，它也应是安全的。他的引申是：开放源代码比封闭源代码更安全，开放源码后可以通过修复已知漏洞，但很多军方的加密都是封闭的，比如北斗的加密等。即不要使用未经证明的加密算法。<br/>
#### 密码学的核心问题
&emsp;&emsp;密码学是研究编制密码和破译密码的技术科学。研究密码变化的客观规律，应用于编制密码以保守通信秘密的，称为编码学；应用于破译密码以获取通信情报的，称为破译学。总称密码学。<br/>
   -  密码学的四个核心问题，包括：<br/> 
       - 保密性： <br/> 
       - 完整性： 数字签名和消息验证码<br/> 
       - 认证：   数字签名<br/> 
       - 不可否认：数字签名<br/> 

&emsp;&emsp;密码学就是研究如何在`不安全的信道上进行安全的通讯`。<br/>
&emsp;&emsp;`数字签名`就是`附加在数据单元上的一些数据,或是对数据单元所作的密码变换`,数字签名技术是将原文通过特定HASH函数得到的摘要信息用发送者的私钥加密，与原文一起传送给接收者。接收者只有用发送者的公钥才能解密被加密的摘要信息，然后用HASH函数对收到的原文提炼出一个摘要信息，与解密得到的摘要进行对比。哪怕只是一个字符不相同，用HASH函数生成的摘要就一定不同。如果比对结果一致，则说明收到的信息是完整的，在传输过程中没有被修改，否则信息一定被修改过，因此数字签名能够验证信息的完整性。<br/>
&emsp;&emsp;`数字签名`一方面是能确定消息的不可抵赖性。发送方是用自己的私钥对信息进行加密的，只有使用发送方的公钥才能解密。另一方面，数字签名能保障消息的完整性。一次数字签名采用一个特定的哈希函数，它对不同文件产生的数字摘要的值也是不相同的。
&emsp;&emsp;`消息认证码`,是一种需要使用密钥的算法，以消息和密钥作为输入，产生一个认证码。拥有密钥的接收方能够计算验证码验证消息的完整性(速度比数字签名快)。<br/>

#### 常用的加密算法（现代密码学算法）
&emsp;&emsp;常用加密算法包括:<br/>
   - 对称加密：加密密钥和解密密钥相同，包括：
       - 序列密码：
          - 序列密码也称为流密码（Stream Cipher），是以一个元素（一个字母或一个比特）作为基本的处理单元。
          - “一次一密”的密码方案是序列密码的雏形。
          - 序列密码涉及到大量的理论知识，提永出了众多的设计原理，也得到了广泛的分析，但许多研究成果并没有完全公开，这也许是因为序列密码目前主要应用革于军事和外交等机密因部门的缘故。目前，公开的序列密码算法主要有RC4、SEAL等。
       - 分组密码：以一定大小作为每次处理的基本单元，使用的是一个不随时间变化的固定变换
          - DES(Data Encryption Standard)算法：
             - 明文按64位进行分组， 密钥长64位，密钥事实上是56位参与DES运算（第8、16、24、32、40、48、56、64位是校验位， 使得每个密钥都有奇数个1）分组后的明文组和56位的密钥按位替代或交换的方法形成密文组的加密方法。
          - AES算法：
             - 分组长度只能是128位，也就是说，每个分组为16个字节（每个字节8位）。密钥的长度可以使用128位、192位或256位。
          - TEA算法：
             - 使用64位的明文分组和128位的密钥
   - 非对称加密：加密密钥和解密密钥不同，包括：
      - 公钥：公开密钥（public key，简称公钥）
      - 私钥：私有密钥（private key，简称私钥）
      - RSA算法：
         - RSA是目前最有影响力的公钥加密算法，它能够抵抗到目前为止已知的绝大多数密码攻击，已被ISO推荐为公钥数据加密标准。
         - 已知只有短的RSA钥匙才可能被强力方式解破，
         - RSA算法基于一个十分简单的数论事实：将两个大素数相乘十分容易，但是想要对其乘积进行因式分解却极其困难，因此可以将乘积公开作为加密密钥。

   - 对称加密：对称密钥的缺点，包括：
      - 密钥分配问题：密续建议一个安全的信道传递密钥
      - 密钥个数问题：n个人互相通信，需要密钥个数为n*(n-1)/2
      - 缺乏不可否认性：电子商务中订单是否真的是用户发的呢？
    
### 2. 分组加密的操作模式
&emsp;&emsp;分组加密算法的共同点是：以一定大小作为每次处理的基本单元，使用的是一个不随时间变化的固定变换，通常一次处理的分组长度为8个字节（DES） 或 16个字节(AES)<br/>
   - 分组密钥算法的操作模式：<br/>
      - 电子密码本(ECB)：<br/>
      - 密码块链接(CBC)：<br/>
      - 填充密码块链接（PCBC）:<br/>
      - 密文反馈（CFB）：<br/>
      - 输出反馈（OFB）：<br/>
      - 计数器模式(CTR):<br/>

&emsp;&emsp;电子密码本(Electronic codebook,ECB)将一个明文分组加密成一个密文分组。因为`相同的明文永远被加密成相同的密文分组`，所以理论上制作一个包含有明文及其对应的密文的密码本是可能的！但是，我们要清楚的了解一点，如果分组的大小为64位，那么密码本就有2<sup>64</sup>项，对于预计算和存储来说，实在是太大了。<br/>
&emsp;&emsp;ECB模式所带来的问题是：如果密码分析者有很多消息的明密文，那它就可以在不知道密钥的情况下编写密码本。在许多实际情况中，有很多消息趋于重复。计算机的产生的消息，如电子邮件，可能有固定的结构。<br/>
   - 针对ECB的攻击，ECB缺点是同样的明文块会被加密成相同的密文块，因此存在如下攻击方式：<br/> 
      - 位图攻击，使得传递的明文图片失去了保密性，不能很好的隐藏数据模式<br/>
      - 替换攻击：ECB加密各字段定长的银行报文(理论上存在)，即容易受到重放攻击的影响<br/>
    
&emsp;&emsp;密码分组链接(cipher-block chaining,CBC)在ECB的基础上，将前一个分组的密文当成后一个分组的输入（异或操作），第一块通过引入初始化向量IV来解决（IV必须足够的随机才行）,因此可以解决ECB的两类缺点。它的主要缺点在于加密过程是串行的，无法被并行化，而且消息必须被填充到块大小的整数倍<br/>
&emsp;&emsp;<br/>

#### CBC 工作模式举例：TEA加密
&emsp;&emsp;TEA的IV：数据填充（随机值），N:密文长度，原始字符串长度+10（填充）+填充字节数n（补齐为N是8的倍数），则N应该是8的倍数<br/>
   - 具体的填充方法：<br/>
      - 第一个字节为：（random() & 0xf8） | n ，这里目的是解密的时候，可以算出来填充的字节数n的值  <br/>
      - 随后填充（n+2）个字节 random()&0xff,后面接原始数据   <br/>
      - 最后填充7个字节0x00，简单的基本数据校验（解密后校验最后7个字节是否全为0）  <br/>
      - 因此一共初始的IV一共是原始字符串长度+10+填充字节数n  （一共是8的倍数）<br/>
   - TEA算法的CBC模式：<br/>
      - 消息被分为多个加密单元，每一个加密单元都是8字节，使用TEA进行加密<br/>
      - 加密结果与下一个加密单元做异或运算后再作为待加密的明文<br/>
      
&emsp;&emsp;10个字节长度的明文，密文长度为10+10+4(填充n)  = 24个字节，最长情况下，密文比明文长度长17个字节(明文7个字节，密文10+7+7=24个字节个字节)

### 3. 非对称密码算法原理
&emsp;&emsp;由于对称密钥的局限性（密钥分配问题，大范围应用场景下密钥维护性差、缺乏不可否认性等），因此考虑非对称加密算法，典型的非对称加密算法包括：
   - 整数分解方案：
      - 因式分解大整数是非常困难的
      - 代表算法：RSA
   - 离散对数方案：
      - Diffie-Hellman密钥交互（DH）
   - 椭圆曲线方案：
      - 椭圆曲线Diffie-Hellman密钥交换（ECDH）
      
### 4. 密钥长度
&emsp;&emsp;加密算法都是经过认证的，操作模式也没有问题的，那加密算法就是安全的么？这块还需要考虑密钥长度，随机计算机性能的提高、分布式计算能力等提升，60位密钥仍然不是足够安全，128位密钥则现在基本可以认为是安全的了。<br/>
&emsp;&emsp;128位密钥当前虽然看是安全的，那10年后呢？还是安全的么？这是不确定的，那么是有一定安全的加密算法呢？理论上一次一密是安全的，但是这种实际操作空间很小（因为要求密钥和明文一样长）<br/>
   - 密钥长度的相关总结：
      - 60位一下都是窗口纸，即DES加密算法是不安全的。
      - \> 80位才安全(下限)，通常要128位密钥才安全
      - 公钥算法的密钥长度
         - 对称算法，密钥是N位，对应的密钥空间就是N位安全级别的(位)
         - 非对称算法，密钥是N位的，对应的密钥空间通常会大于N位安全级别的（位），和具体算法的数据原理有关。

## 二、 随机数发生器  
### 1. 随机数发生器
   - 随机数发生器具备以下三个属性：<br/>
      - 统计规律上是随机的：看起来是具备随机性的，例如掷骰子
      - 不可预测下：
      - 不能被可靠的重复产生：
      
   - 随机数发生器的分类：<br/>
      - 真随机数发生器TRNG(True Random Number Generator) ： 掷骰子动作就是真随机数发生器
         - 不可重复产生
         - 不可预测
         - 看起来随机
      - 伪随机数发生器PRNG（Pseudo Random Number Generator）
         - 看起来随机  ： Rand()函数，种子固定的，产生的序列是可预测的，因此密码学上不能用
      - 密码学安全随机数发生器（CSPRNG，Cryptographically Secure Pseudo Random Number Generator）
         - 不可预测
         - 看起来随机
      - 具体的产生随机数的算法
         - rand()   java.util.random
         - /dev/urandom   /dev/random  :推荐
         - fortuna yarrow   密码学上随机数发生器算法，例如mac采用了yarrow算法？

### 2. 信息熵
   - 信息熵：<br/>
      - 香农，信息论的奠基人
      - 证明了熵与内容的不确定程度有等价关系：
      - 信息熵公式：H(x) = E[I(xi)] = E[ log(2,1/p(xi)) ] = -∑p(xi)log(2,p(xi)) (i=1,2,..n)
      - 以rand()举例，计划产生16个字节的随机数，假设采用rand()（srand(time(null))）的方式，假设该端代码实在某天上午运行的（比如抽奖场景），则可能的时间种子粒度每秒执行的，即6*3600种，假设是设置的随机数是概率的，如果暴力破解，其对应的信息熵是：-∑p(xi)log(2,p(xi)) (i=1,2,..,6\*3600,p(xi) = 1\/6\*3600) 计算结果熵是多大的呢log<sub>2</sub>6\*3600 约等于 15bit,即从密码学的密钥长度评价，安全性是远远不够的。即便srand（）的参数是4个字节全部设置了，则熵才32位而已，即不是安全的。
      
      
## 三、 用户密码(口令)的安全
&emsp;&emsp;密码的安全由两方面来保证，一方面是`密码的强度`，另一方面则是`存储安全`<br/>
   - 密码的强度:
      - 从信息熵的角度来评估密码的强度，等概率情况下:`-H = L \* log<sub>2</sub>N (L:密码长度，N：密码包含字符的种类)`，即密码更长，更复杂就越安全。
      - 但是用户是有偏好的，例如密码设置为8888888888，即每种密码的概率不等，导致熵减小。
   - 存储安全：
      - 明文： A站被拖库，明文存储肯定完蛋了
      - Hash : md5、SHA
         - hash函数的特性：
            - 单项不可逆： 密钥空间不一样；HASH固定长度输出后，包含的熵实际是变小的，即不可能通过逆向得到原来的值了
            - 输出固定长度
            - 输入发生很小变化，输出也很大不同
         - Hash函数的安全性从3个方面来衡量：
            - 抗第一原相性：x->y，给定一个y能否找到x？ 即是否可逆
            - 抗第二原相性：x1->y,x->y,给定一个y,能否找到（构造出）x1呢？
            - 抗冲突性 ： 因为hash（md5）的取值空间有限，一定会有冲突（肯定保证不了，只有强弱的关系），能否找到x,x1,让x->y,x1->y
               - 举例：一间教室最少有多少名学生，才能使得有两个学生的生日在同一天的概率大于等于1/2？
                  - p(n) = 1(1-1/365)(1-2/365)...（1-n-1/365） = 365/365 \* 364/365 \* 363/365...\*365-n+1/365 = 365!/(365<sup>n</sup>\*(365-n)!)
                  - p = 1-p(n) = 1-365!/(365<sup>n</sup>\*(365-n)!)
               - 举例2：生日问题应用于检测哈希函数
                  - N位长度的哈希表可能发生碰撞测试次数不是2<sup>N</sup>次，而是只有2<sup>N/2</sup>次
            - Hash算法的单向性，适合用于保存密码
            - 冲突攻击对密码存储不构成威胁
            - 主要威胁来自于彩虹表（hash计算快，构造彩虹表的时间复杂度低，门槛低）
      - Salted Hash
         - 给密码加一个随机的前缀或者后缀，然后再进行hash,这个随机的后缀或者前缀称为“盐”
         - 用来规避彩虹表的威胁（代价变大，要为每个用户场景创建一个彩虹表），同一个密码，每次加盐不同，密文结果不同
         - 盐 的使用注意事项：
            - 用户每次创建或者修改密码一定要使用一个新的随机盐
            - 盐的大小要跟hash函数的输出一致，如果盐的bit太小（熵小），就很容易构造全量的彩虹表进行攻击（代价低）
            - 不用用用户名做盐（部分高价值用户，比如root,是值得为他创建一个彩虹表）
            - 盐要使用密码学上的可靠安全的伪随机数发生器来产生
      - Key stretching
         - 加盐可以防止批量破解（比如，对不同用户采用不同的盐）
            - 盐的安全性不需要保密，密码登录的时候，盐需要明文给到客户端
            - 如果盐泄露，也不会有太大问题，就是因为 彩虹表仍然可以对 单个用户进行攻击的（相对于全局，安全性是可靠的）
         - 针对单个hash的攻击依然有效
         - 基本思路就是让每次鉴权的时间复杂度达到刚刚好，使得正常用户的体验能够接受，但是黑客暴力破解或者构建彩虹表的成本大幅度提高。
         - 使用标准算法PBKDF2，bcrypt,scrypt
            - Key stretching-Bcrypt:
               - 基于Blowfish加密算法变形而来
               - 通过参数（work factor）调整计算强调
               - 广泛的函数库支持：C、java,objective c,js,perl,python,php,c#等

&emsp;&emsp;实际上，例如www.cmd5.com 网站，输入md5给出加密前的明文？Hash算法是如何破解明文的呢？<br/>
   - 算法是满足抗第一原相性（不可逆的），对应的破解技术方法主要有：
      - 暴力计算：空间复杂度小
         - 假设密码长度和密码字符的组成，采用暴力破解，相对不是很难
      - 字典攻击：时间复杂度小
         - ？
      - 彩虹表： 平衡时空复杂度
         - 要破解md5,就构造md5的彩虹表，要破解sha1，就构造sha1的彩虹表，因此对各种加密算法的适配性是强耦合的
         - 经过反复的H-R变换，R函数要如何构造？（R函数如果一样的话， 会导致彩虹表链中存储的信息是重复的，因为H-R都一样了，也可能导致链与链之间的重复率很高）
         - 彩虹表，现有的方案，www.freerainbowtables.com，基本的成功率在99.9%的
       

## 四、 参考文献
   - [<传统密码技术>](https://blog.csdn.net/gscienty/article/details/53382169)
   - [《腾讯内部密码学基础课件》](http://km.oa.com/group/18092/articles/show/405622)