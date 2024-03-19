## 链表

用数组模拟链表

单链表的基本操作：

```c++
#include<iostream>
using namespace std;

const int N = 100010;

int head, e[N], ne[N], idx;//head表示头节点，idx表示将要使用第idx个节点

void init(){
    head = -1;
    idx = 1;
}//链表初始化

void add_to_head(int x){
    e[idx] = x;
    ne[idx] = head;
    head = idx;
    idx++;
}//将加到head前面

void Delete (int k){
    ne[k] = ne[ne[k]];
}//删除k节点

void add_to_k(int k, int x){
    e[idx] = x;
    ne[idx] = ne[k];
    ne[k] = idx;
    idx++;
}在k节点后面添加一个节点

```

双链表的基本操作：

```c++
#include <iostream>
using namespace std;
const int N = 100010;
int e[N], l[N], r[N], idx;//e表示某个节点存的值，l表示某个节点左边的位置，r表示右边的位置，idx表示将要使用第idx个节点

//双链表初始化
void init(){
    r[0] = 1;
    l[1] = 0;
    idx = 2;
}//这里的0和1分别代表链表的起点和终点，而且第0个和第1个节点已经被使用，因此idx从2开始变更。

//在节点k右侧插入一个节点
void add(int k, int x){
    e[idx] = x;
    l[idx] = k;
    r[idx] = r[k];
    l[r[k]] = idx;
    r[k] = idx;
    idx++;
}

//删除k节点
void remove(int k){
    l[r[k]] = l[k];
    r[l[k]] = r[k];
}//若想删除第k个节点，则应该调用remove(k+1)，因为idx从2开始增加

```

## 栈和队列

### 1.栈

先进后出

用数组模拟栈：

```c++
#include <iostream>
using namespace std;
const int N = 100010;
int stack[N], tt;
//输入
stk[++tt] = x;

//弹出
tt--；
  
//判断是否为空栈
if(tt > 0)
```

同时，c++ stl库也有封装好的栈可以使用

#### [单调栈](https://www.acwing.com/problem/content/832/)

```c++
#include <iostream>
#include <stack>
using namespace std;
const int N = 100010;
int arr[N];

int main(){
    ios::sync_with_stdio(false);
    int n;
    cin >> n;
    for(int i = 0;i < n;i++)
        cin >> arr[i];
    stack<int> stk;
    stk.push(-1);//先讲最小的-1压进栈
    for(int i = 0;i < n;i++){
        while(arr[i] <= stk.top()){
            stk.pop();
        }
        cout << stk.top() << ' ';
        stk.push(arr[i]);
    }
    return 0;
}
```



### 2.队列(queue)

先进先出(对头出队，队尾入队)

```c++
#include<iostream>
using namespace std;

const in N = 1e6;
int q[N], head, tail;

void init(){
  head = 0;
  tail = 0;
}

void push(int x){
  q[++tail] = x;
}

void pop(int x){
  head++;
}

bool isEmpty(){
  if(head>=tail)
    return true;
  else
    return false;
}
```

#### [单调队列典型:sliding window](https://www.acwing.com/problem/content/156/)

### 3.KMP

KMP算法：用来解决寻找字串的问题

在brute force解这类问题时常常使用二重for循环：

```c++
for(int i = 1;i <= n;i++)
  for(int j = i+1;;j <= n;j++){
    ...
  }
```

当匹配到某一点时，若两个字符不相等， 则直接退出该层循环。kmp算法可以利用这个点之前已经匹配好的部分来降低时间复杂度。

源码

```c++
#include <iostream>
using namespace std;
const int N = 100010;
char s[N], p[N];
int ne[N];

int main(){
    int n, m;
    cin >> n >> p + 1 >> m >> s + 1;
    for(int i = 2, j = 0;i < n;i++){
        while(j&&p[i]!=p[j+1])
            j = ne[j];
        if(p[i] == p[j+1])
            j++;
        ne[i] = j;
    }//求ne数组
    for(int i = 1, j = 0;i <= m;i++{
        while(j&&s[i]!=p[j+1])
            j = ne[j];
        if(j == n){
            cout << i - n << ' ';
            j = ne[j];
        }
    }//匹配过程
}

```

#### 1.ne[N]数组的含义

#### ne[i]的含义，即模式串1～i部分，满足前缀与后缀相等的最大长度。

例："aabaabaaf" 对应的ne数组：

`ne[1] = 0;`

`ne[2] = 1;`

`ne[3] = 0;`

`ne[4] = 1;`

`ne[5] = 2;`

`ne[6] = 3;`



#### 2.利用ne数组匹配的过程

假如在某一点不匹配，而前面均匹配，将模式串后退到前面匹配好的部分到ne数组对应的地址。

#### 3.求ne数组

与匹配的过程类似，注意`ne[1]=0`，从2开始求ne数组



