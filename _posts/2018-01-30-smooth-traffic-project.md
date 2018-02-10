---
layout:     post
title:      "畅通工程"
subtitle:   "我的第一个并查集程序"
date:       2018-01-30
author:     "JinTao"
header-img: "img/head2.jpg"
catalog: true
tags:
- ACM
- 并查集
---

## 畅通工程

### 描述
某省调查城镇交通状况，得到现有城镇道路统计表，表中列出了每条道路直接连通的城镇。省政府“畅通工程”的目标是使全省任何两个城镇间都可以实现交通（但不一定有直接的道路相连，只要互相间接通过道路可达即可）。问最少还需要建设多少条道路？ 

### 输入
测试输入包含若干测试用例。每个测试用例的第1行给出两个正整数，分别是城镇数目N ( < 1000 )和道路数目M；随后的M行对应M条道路，每行给出一对正整数，分别是该条道路直接连通的两个城镇的编号。为简单起见，城镇从1到N编号。 
注意:两个城市之间可以有多条道路相通,也就是说 
3 3 
1 2 
1 2 
2 1 
这种输入也是合法的 
当N为0时，输入结束，该用例不被处理。 
### 输出
对每个测试用例，在1行里输出最少还需要建设的道路数目。
### 样例输入1 
4 2<br>
1 3<br>
4 3<br>
3 3<br>
1 2<br>
1 3<br>
2 3<br>
5 2<br>
1 2<br>
3 5<br>
999 0<br>
0

### 样例输出1 
1<br>
0<br>
2<br>
998

### AC
``` cpp
#include<iostream>

using namespace std;
int f[1010];
int find(int x)
{
	if(f[x]==x) return x;
	else	return	f[x]=find(f[x]);
}
void unit(int a,int b)
{
	int a1=find(a);
	int b1=find(b);
	if(a1!=b1)	f[a1]=b1;
}
int main()
{
	int n;
	while(cin>>n&&n)
	{
		for(int i=1;i<=n;++i)	f[i]=i;
		int m;cin>>m;
		int a,b;
		while(m--)
		{
			cin>>a>>b;
			unit(a,b);
		}
		int cnt=0;
		for(int i=1;i<=n;i++)
		{
			if(f[i]==i) cnt++;
		}
		cout<<cnt-1<<endl;
	}
	return 0;
}
```
