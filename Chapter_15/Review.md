# 第十五章复习题

#### 1. 数据压缩方法有哪两种类别？

有损压缩，无损压缩

#### 2. 无损压缩和有损压缩有什么不同？

有损压缩解压缩后跟压缩前的数据会有差别，而无损压缩不会。

#### 3. 什么是游程长度编码？

将连续重复出现的单个字符（或数位）替换为该字符（或数位）的计数

#### 4. LZ编码方法是怎样减少需要传输的为的数量的？

通过建立一个通信双方共用的字典，然后用发送字典索引代替发送文本本身来压缩数据量

#### 5. 什么是赫夫曼编码？

赫夫曼编码是使用根据字符出现频率构建的赫夫曼树对字符的编码

#### 6. 字典在LZ编码中担当什么角色？

担任压缩和解压缩的数据对照表的角色

#### 7. 相对于赫夫曼编码，LZ编码的优点是什么？

随着传输次数的增多，LZ编码的压缩率会逐渐提高，而赫夫曼编码的压缩率是一直不变的。

#### 8. 有损压缩的三种方法是什么？

JPEG，MPEG，MP3

#### 9. 什么时候用JPEG格式？什么时候用MPEG格式？

图像压缩使用JPEG，视频压缩使用MPEG

#### 10. JPEG和MPEG有什么关系？

MPEG中的空间压缩使用了JPEG

#### 11. 在JPEG格式中分块有什么作用？

减少离散余弦变换的运算量

#### 12. 在JPEG格式中为什么需要离散余弦变换？

通过离散余弦变换使得块中的数据有大量的0，从而使这些0可以被压缩

#### 13. 量化对于数据压缩有何贡献？

将浮点数转化为限定范围内的整数，从而减少单个数值所占的存储空间

#### 14. 在MPEG压缩中什么是帧？

视频的本质是许多图片的快速切换，其中单张图片即为帧

#### 15. 相对于时间压缩而言空间压缩是什么？

空间压缩仅考虑单个帧本身的图片压缩

#### 16. 讨论MPEG格式中三种不同类型的帧

I-帧：包含完整的帧信息

P-帧：信息只包含当前帧对比上一个I-帧或P-帧的增量

B-帧：信息只跟前后的I-帧或P-帧有关