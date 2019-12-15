# 第十五章 数据压缩

本章主要介绍一些常用的数据压缩算法，包括有损压缩和无损压缩

## 无损压缩

无损压缩适用于文本等无法容忍信息丢失的数据。

### 游程长度编码

简单的讲就是将数据串改为**数据计数串**，例如说`BBBBBBAAAA`改为`B06A04`。

这种方法对字符集越少的串越有效，尤其是1出现的次数较少的01串。

这里我们规定将1当做分隔符，而只记0的数量，并只使用4位二进制数字计数。

#### 例子

```
000000000000001000011000000000000 -> 1110 0100 0000 1100
```

其实可以理解为：14个0，然后有个1，再有4个0，然后有个1，再有0个0，然后有个1，再有12个0。

#### 溢出情况处理

这种方法会遇到一个问题就是，当0的个数超过15个的时候怎么处理。

这里默认当一个计数是1111的时候，后面跟着的计数并没有1隔开：

```
00000000000000000000 -> 1111 0101
```

译码的时候遇到1111的时候就不会补1了。

#### 边界情况处理

溢出情况处理方式就又会引入一个问题：如果0的个数恰好是15个呢？

这个时候就需要跟一个0000表示结束了：

```
00000000000000010000 -> 1111 0000 0100
```

### 赫夫曼编码

适用于文本编码。根据字符出现频率构建赫夫曼树，通过赫夫曼树得到编码表。

### Lempel Ziv编码

这种编码的适用场景为两个客户端之间的文本传输的压缩。

初始思路是，假设对话双方都有一本字典，那么其就可以通过字典进行压缩和解压缩文本信息。

但问题在于难以构造一本通用的字典，不同的两个人对话使用的词频是不一样的。

Lempel Ziv编码可以看做是一种自适应字典生成。其压缩串本身自带了字典信息。

#### 例子

以串`BAABABBBAABBBBAA`为例

+ 首先创建一个空字典（或者使用已有字典）

+ 读取第一个字符B，发现其不在字典中，将其加入字典并编号为1：

| 1    |
| ---- |
| B    |

+ 读取第二个字符A，发现其不在字典中，将其加入字典并编号为2：

| 1    | 2    |
| ---- | ---- |
| B    | A    |

+ 读取第三个字符A，发现其在字典中，于是继续读取第四个字符B，发现AB不在字典中，于是将AB编码为2B并加入字典，编号为3：

| 1    | 2    | 3    |
| ---- | ---- | ---- |
| B    | A    | AB   |

+ 从第5个字符开始读取至第一次字典中不存在这个字符串（也就是ABB），于是将ABB编码为3B并加入字典，编号为4：

| 1    | 2    | 3    | 4    |
| ---- | ---- | ---- | ---- |
| B    | A    | AB   | ABB  |

+ 从第8个字符开始读取至第一次字典中不存在这个字符串（也就是BA），于是将BA编码为1A并加入字典，编号为5：

| 1    | 2    | 3    | 4    | 5    |
| ---- | ---- | ---- | ---- | ---- |
| B    | A    | AB   | ABB  | BA   |

+ 从第10个字符开始读取至第一次字典中不存在这个字符串（也就是ABBB），于是将ABBB编码为4B并加入字典，编号为6：

| 1    | 2    | 3    | 4    | 5    | 6    |
| ---- | ---- | ---- | ---- | ---- | ---- |
| B    | A    | AB   | ABB  | BA   | ABBB |

+ 从第14个字符开始读取至第一次字典中不存在这个字符串（也就是BAA），于是将BAA编码为5A并加入字典，编号为7：

| 1    | 2    | 3    | 4    | 5    | 6    | 7    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| B    | A    | AB   | ABB  | BA   | ABBB | BAA  |

至此，字符串就会被压缩为`B,A,2B,3B,1A,4B,5A`。

借此我们可以推断：

+ 对方解码的时候也可以获得同样的字典，于是便可以完成字典同步。
+ 同一个字符串再发送一次的时候会被压缩的更小

## 有损压缩

图片，视频，音频这些文件由于人类的生理极限和需求，故可以接受有损压缩。

### 图像压缩：JPEG

JPEG主要是利用现实图像经常出现较为连续的像素块的思路，利用离散余弦变换进行压缩。

其四个步骤为：

+ 分块：由于离散余弦变换是一个O(n^2)的算法，直接整张图去变换显然不现实（而且可预见的效果肯定不好），故需要将图片切成若干个8*8的块。
+ 离散余弦变换：针对每个块进行离散余弦变换运算
+ 量化：将每个数除以一个常量使数字范围变小，并去掉小数点后的位数
  + 就是这一步会导致损失
+ 压缩：对于每个块而言，如果这个块颜色差不多，那么其数值主要集中在左上角，而右下角基本都是零。于是利用这个特性可以用蛇形的方法（从左上角到右下角的蛇形）将块展开成一个数列。那么这个数列后面基本都是0，于是就可以将这些0去掉。

### 视频压缩：MPEG

视频本身就可以看作是许多图像叠在一起，于是其本身就可以使用JPEG的方式压缩每一帧。

除此之外视频也可以用帧分类的方式从时间维度上压缩视频。

在这里我们把帧分为三类：

+ I-帧：包含完整的图片信息（当然其是经过JPEG压缩后的）
+ P-帧：仅记录其与前面的I-帧相比的变化
+ B-帧：与前面和后续的I-帧或P-帧有关系，相当于记录两者的中间态。

于是便不需要每一帧都存完整的图像，只需要将帧合理分类便可以缩小存储量（P-帧和B-帧的存储量小于I-帧）
