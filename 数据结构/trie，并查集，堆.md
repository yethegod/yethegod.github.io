## trie(字典树)

### 1.trie的作用

通过查询前缀快速查找某一个字符串

### 2.trie的代码实现

```c++
#include <iostream>
using namespace std;
const int N = 100010;

int son[N][26], cnt[N], idx;

void insert(char str[]){
    int p = 0;
    for(int i = 0;str[i];i++){
        int u = str[i] - 'a';
        if(!son[p][u])
            son[p][u] = ++idx;
        p = son[p][u];
    }
    cnt[p]++;
}

int query(char str[]){
    int p = 0;
    for(int i = 0;str[i];i++){
        int u = str[i] - 'a';
        if(!son[p][u])
            return 0;
        p = son[p][u];
    }
    return cnt[p];
}
```

代码解读：

idx的含义是当前已经用到的下标(可以理解为每个元素的编号)

`son[N][26]`数组存储的是每一个节点的子元素的绝对下标

`cnt[x]`存储的是以某编号为x的元素结尾的字符串数量

[二进制的字典树](https://www.acwing.com/problem/content/description/145/)：最大异或对

## 并查集

### 1.并查集的作用

1. 将两个元素合并

2. 询问两个元素是否在同一节点

### 2.代码实现

```c++
#include<iostream>
using namespace std;

const int N = 100010;
int p[N];

int find(int x){
    if(p[x]!=x) p[x] = find(p[x]);
    return p[x];
}

void Merge(int a, int b){
    if(find(a)==find(b))
        return;
    p[find(a)] = find(b);
}

bool query(int a, int b){
    return (find(a)==find(b))? true : false;
}
int main(){
    int n, m;
    cin >> n >> m;
    for(int i = 1;i <= n;i++)
        p[i] = i;
    while(m--){
        char op;
        int a, b;
        cin >> op >> a >> b;
        if(op =='M')
            Merge(a, b);
        else if(op == 'Q')
            cout << (query(a, b) ? "Yes" : "No") << endl;
    }
}
```

1. find函数的作用：找到x的祖宗节点
2. merge函数：使其中一个数的祖宗节点是另一个数的祖宗节点的父节

[合并集合](https://www.acwing.com/problem/content/838/) 

### 2.进阶的并查集

[连通块中点的数量](https://www.acwing.com/activity/content/problem/content/886/ )



## 3.堆

### 1.基本结构

完全二叉树

1. 除了最后一层节点外都是满节点
2. 最后一层节点从左到右排列，中间没有空节点

### 2.代码

以小根堆为例 (小根堆：指每个根节点是三个节点中最小的那个)

[堆排序](https://www.acwing.com/problem/content/840/)

```c++
#include<iostream> 
#include<algorithm>

using namespace std;

const int N = 100010;

int h[N], mySize;

int n, m;

void down(int u){
    int t = u;
    if (2 * u <= mySize && h[t] > h[2 * u])
        t = 2 * u;
    if (2 * u + 1 <= mySize && h[t] > h[2 * u + 1])
        t = 2 * u + 1;
    if (u != t)
    {
        swap(h[u], h[t]);
        down(t);
    }
}

void up(int u){
  while(u/2&&h[u/2]>=h[u]){
    swap(h[u/2],h[u]);
    u /= 2;
  }
}
int main()
{
    cin >> n >> m;
    mySize = n;
    for (int i = 1; i <= n; i++)
        scanf("%d", &h[i]);
    for (int i = n / 2; i; i--)
        down(i);

    while (m--)
    {
        cout << h[1] << " ";
        h[1] = h[mySize--];
        down(1);
    }

    return 0;
}
```

1. down函数的原理：和左子节点(2*k)比较，再和右子节点(2k+1)比较，调换后向下递归
2. up函数的原理：只要有父节点，就一直向上比较
3. 如何排序：

* 将h[1]输出(总是最小值)
* 将h[1]与堆的最后一个节点删除
* 再重新调用down函数
