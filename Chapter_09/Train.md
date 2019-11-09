# 第九章练习题

#### 第1题

```
int a, b, c;
```

#### 第2题

```
double a = 1.1;
double b = 4.5;
double c = 1.4;
```

#### 第3题

```
const char a = 'a';
const int b = 1;
const double c = 3.14;
```

#### 第4题

因为常量一经定义就不能修改。如果不在定义的时候初始化的话，那么其就会变成一个无法被修改的没有值（或者值是混乱的）的量，显然这样的量是没有用的。

#### 第5题

2次

#### 第6题

理论上的正无穷次，实际上试A的数据类型而定，直到A发生溢出之前都会一直循环。

#### 第7题

8次

#### 第8题

5次

#### 第9题

```
A = 5
do
{
	statement;
	A = A - 2;
}while(A < 8)
```

#### 第10题

```
int i = 5;
do
{
	statement;
	i = i + 1;
	i++;
}while(i < 20)
```

#### 第11题

```
int i = 5;
while(i < 20)
{
	statement;
	i = i + 1;
	i++;
}
```

#### 第12题

```
for(A = 5; A < 10; A = A + 1)
{
	statement;
}
```

#### 第13题

```
for(A = 5; A < 8; A = A - 2)
{
	statement;
}
```

#### 第14题

```
while(false)
{
	statement;
}
```

#### 第15题

无法做到。因为do循环不论如何都会执行至少一次循环体

#### 第16题

```
for(;false;)
{
	statement;
}
```

#### 第17题

```
while(true)
{
	statement;
}
```

#### 第18题

```
do
{
	statement;
}while(true)
```

#### 第19题

```
for(;true;)
{
	statement;
}
```

#### 第20题

```
12
4
5
```

#### 第21题

```
变量：Hello
字面值："Hello"
```

#### 第22题

```
switch(A)
{
	case 4:
		statement1;
		break;
	case 6:
		statement2;
		break;
	case 8:
		statement3;
		break;
}
```

#### 第23题

A和B传值，S和P传引用

#### 第24题

A和B传值，S传引用

#### 第25题

传值

#### 第26题

传引用

#### 第27题

传值