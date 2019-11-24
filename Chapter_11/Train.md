# 第十一章练习题

从这章的练习题开始，所有涉及到写算法的题目都会使用C++来写。

~~我不写伪代码啦JOJO！！！！~~

#### 第1题

```c++
bool Check(int A[], int B[])
{
		for(int i = 0; i < 10; i++)
		{
				if(A[i] != B[i])
				{
						return false;
				}
		}
		return true;
}
```

#### 第2题

```c++
void Reverse(int A[], int len)
{
		for(int i = 0; i < len - i - 1; i++)
		{
				int pos = len - i - 1;
				int tmp = A[i];
				A[i] = A[pos];
				A[pos] = tmp;
		}
}
```

#### 第3题

```c++
void Print(int A[][], int R, int C)
{
		for(int i = 0; i < R; i++)
		{
				for(int j = 0; j < C; j++)
				{
						printf("%d ", A[i][j]);
				}
				printf("\n");
		}
}
```

#### 第4题

```c++
int Find(int elem, int A[], int len)
{
		for(int i = 0; i < len; i++)
		{
				if(A[i] == elem)return i;
		}
		return -1;
}
```

#### 第5题

```c++
int LowerBound(int elem, int A[], int len)
{
		int l = 0, r = len - 1;
		while(l < r)
		{
				int mid = (l + r) >> 1;
				if(A[mid] >= elem) r = mid;
				else l = mid + 1;
		}
		return l;
}
```

#### 第6题

```c++
void Insert(int elem, int A[], int &len)
{
		int pos = LowerBound(elem, A, len);
		for(int i = len; i > pos; i--)
		{
				A[i] = A[i - 1];
		}
		A[pos] = elem;
  	len++;
}
```

#### 第7题

```c++
void Delete(int elem, int A[], int &len)
{
		int pos = LowerBound(elem, A, len);
		if(A[pos] != elem)return;
		for(int i = pos; i < len - 1; i++)
		{
				A[i] = A[i + 1];
		}
		len--;
}
```

#### 第8题

```c++
void Multi(int A[], int len, int C)
{
		for(int i = 0; i < len; i++)
		{
				A[i] *= C;
		}
}
```

#### 第9题

```c++
struct Fraction
{
		int nume;
		int deno;
};

int gcd(int a, int b)
{
		if(b == 0)return a;
		return gcd(b, a%b);
}

int abs(int a)
{
		if(a < 0)return -a;
		return a;
}

Fraction Add(Fraction Fr1, Fraction Fr2)
{
		Fraction ret;
		ret.deno = Fr1.deno * Fr2.deno;
		ret.nume = Fr1.nume * Fr2.deno + Fr1.deno * Fr2.nume;
		int g = gcd(abs(ret.deno), abs(ret.nume));
		ret.deno /= g;
		ret.nume /= g;
		return ret;
}
```

#### 第10题

```c++
struct Fraction
{
		int nume;
		int deno;
};

int gcd(int a, int b)
{
		if(b == 0)return a;
		return gcd(b, a%b);
}

int abs(int a)
{
		if(a < 0)return -a;
		return a;
}

Fraction Sub(Fraction Fr1, Fraction Fr2)
{
		Fraction ret;
		ret.deno = Fr1.deno * Fr2.deno;
		ret.nume = Fr1.nume * Fr2.deno - Fr1.deno * Fr2.nume;
		int g = gcd(abs(ret.deno), abs(ret.nume));
		ret.deno /= g;
		ret.nume /= g;
		return ret;
}
```

#### 第11题

```c++
struct Fraction
{
		int nume;
		int deno;
};

int gcd(int a, int b)
{
		if(b == 0)return a;
		return gcd(b, a%b);
}

int abs(int a)
{
		if(a < 0)return -a;
		return a;
}

Fraction Multi(Fraction Fr1, Fraction Fr2)
{
		Fraction ret;
		ret.deno = Fr1.deno * Fr2.deno;
		ret.nume = Fr1.nume * Fr2.nume;
		int g = gcd(abs(ret.deno), abs(ret.nume));
		ret.deno /= g;
		ret.nume /= g;
		return ret;
}
```

#### 第12题

```c++
struct Fraction
{
		int nume;
		int deno;
};

int gcd(int a, int b)
{
		if(b == 0)return a;
		return gcd(b, a%b);
}

int abs(int a)
{
		if(a < 0)return -a;
		return a;
}

Fraction Divide(Fraction Fr1, Fraction Fr2)
{
		Fraction ret;
		ret.deno = Fr1.deno * Fr2.nume;
		ret.nume = Fr1.nume * Fr2.deno;
		int g = gcd(abs(ret.deno), abs(ret.nume));
		ret.deno /= g;
		ret.nume /= g;
		return ret;
}
```

#### 第13题

> 画示意图？很好。
>
> 但是我拒绝！
>
> 用一个结构体就可以完成的事情要用示意图？？

```c++
struct Student
{
		string Identify;
		string Name;
		int Grade;
};

struct StudentNode
{
		Student student;
		StudentNode *nxt;
};
```

#### 第14题

> 不是11.5吗。。

进入`pre = null`分支，将`(*cur).link`，也就是`NULL`赋值给list并返回。

#### 第15题

> 不是11.4吗。。

进入`list = null`分支，创建一个新的节点（头节点）。

再进入`pre = null`分支，将list的link赋值为新加入的节点的地址。

#### 第16题

额。。这题不是跟第15题重了吗。。

#### 第17题

```c++
struct Node
{
		int elem;
		Node *nxt;
};

int Average(Node *list)
{
		int cnt = 0, sum = 0;
		list = list -> nxt;	// 忽略头节点
		while(list != NULL)
		{
				cnt++;
				sum += list -> elem;
				list = list -> nxt;
		}
		if(cnt != 0)sum /= cnt;
		return sum;
}
```

#### 第18题

将链表指针赋值为其头节点的指向下一个节点的指针，这意味着链表的头节点被舍弃，其下一个节点成为头节点。

#### 第19题

pre和cur都会指向其原先指向的节点的下一个节点。

