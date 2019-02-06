---
title: ACM-ICPC 2018 徐州赛区网络预赛 
---
```
Time Limit: 1000ms       Memory Limit: 262144KB 
```
### Description 
 Mur loves hash algorithm, and he sometimes encrypt another one’s name, and call him with that encrypted value. For instance, he calls Kimura KMR, and calls Suzuki YJSNPI. One day he read a book about SHA-256, which can transit a string into just 256 bits. Mur thought that is really cool, and he came up with a new algorithm to do the similar work. The algorithm works this way: first we choose a single letter L as the seed, and for the input(you can regard the input as a string s, s[i] represents the i th character in the string)we calculates the value(|(int) L – s[i]|), and write down the number(keeping leading zero. The length of each answer equals to 2 because the string only contains letters and numbers). Numbers writes from left to right, finally transfer all digits into a single integer(without leading zero(s)). For instance, if we choose ‘z’ as the seed, the string “oMl” becomes “11 45 14”.  It’s easy to find out that the algorithm cannot transfer any input string into the same length. Though in despair, Mur still wants to know the length of the answer the algorithm produces. Due to the silliness of Mur, he can even not figure out this, so you are assigned with the work to calculate the answer. 
### Input 
 First line a integer T, the number of test cases(T <= 10)  For each test case:  First line contains a integer N and a character z, (N <= 1000000)  Second line contains a string with length N. Problem makes sure that all characters referred in the problem are only letters. 
### Output 
 A single number which gives the answer. 
 
### Sample input 
2 
3 z 
oMl
6 Y 
YJSNPI 
 
### Sample output 
6 
10 
## 翻译
```
Mur喜欢哈希算法，他有时加密另一个人的名字，然后用加密值给他打电话。例如，他打电
话给Kimura KMR，并打电话给Suzuki YJSNPI。有一天，他读了一本关于SHA-256的
书，它可以将字符串转换成256位。 Mur认为这很酷，他想出了一个新的算法来完成类似的
工作。算法以这种方式工作：首先我们选择单个字母L作为种子，对于输入（您可以将输入
视为字符串s，s [i]表示字符串中的第i个字符）我们计算值（ |（int）L - s [i] 
|），并记下数字（保持前导零。每个答案的长度等于2，因为字符串只包含字母和数字）。
数字从左到右写入，最后将所有数字转换为单个整数（不带前导零）。例如，如果我们选
择'z'作为种子，则字符串“oMl”变为“11 45 14”。很容易发现该算法无法将任何输入字
符串转换为相同的长度。虽然在绝望中，Mur仍然想知道算法产生的答案的长度。由于穆尔
的愚蠢，他甚至无法弄清楚这一点，所以你被分配了计算答案的工作。
```
### 输入
 第一行是整数T，测试用例数（T <= 10）对于每个测试用例：第一行包含整数N和字符z，（N <= 1000000）第二行包含长度为N的字符串。确保问题中提到的所有字符都只是字母。
### 输出
 一个数字给出了答案。
 
### 样本输入
2 
3 z 
oMl 
6 Y 
YJSNPI
 
### 样本输出
6 
10

> 水题，但是特别坑。 
> 这里先讲第二个样例： 减出来的结果是  00  15  06  11  09  16 
> 这样去除前面的0，得出来的结果就是1506110916，这10位
> 如果全部都是0呢 比如 <br>4 z<br>zzzz<br> 这个时候就要输出 1 而不是 0

```
#include <iostream>
#include <cstdio>
#include <string>
#include <cstring>
#include <vector>
#include <set>
#include <algorithm>
#include <cstdlib>
#include <functional>
#include <cmath>
using namespace std;
int main()
{
	int T;
	cin >> T;
	while(T--){
		int sum = 0;
		int len;
		char Seed, s;
		cin >> len >> Seed;
        bool flag = false, fir = true;
		for(int i=0; i<len; i++){
			cin >> s;
			int t = Seed - s;
			t = abs(t);
            if(t != 0)
                flag = true;
        	if(flag){
                if(fir){
                    if(t >= 1 && t <= 9)
                        sum += 1;
                    else 
                        sum += 2;
                    fir = false;
                }
                else sum += 2;
            }
		}
        if(flag == false)
            sum = 1;
		cout << sum << endl;
	} 
	return 0;
}
```

### Description 
 Ryuji is not a good student, and he doesn’t want to study. But there are n books he should learn, each book has its knowledge a[i]. Unfortunately, the longer he learns, the fewer he gets. That means, if he reads books from l to r, he will get a[l]*L+a[l+1]*(L-1)+…+a[r1]*2+a[r] (L is the length of [l, r] that equals to r-l+1).  Now Ryuji has q questions, you should answer him: 1. If the question type is 1, you should answer how much knowledge he will get after he reads books [l, r] 2. If the question type is 2, Ryuji will change the ith book’s knowledge to a new value. 
 
### Input 
 First line contains two integers n and q (n, q <= 100000).  The next line contains n integers represent a[i]( a[i] <= 1e9)  Then in next q line each line contains three integers a, b, c, if a = 1, it means question type is 1, and b, c represents [l, r]. if a = 2, it means question type is 2, and b, c means Ryuji changes the bth book’ knowledge to c. 
 
### Output 
 For each question, output one line with one integer represent the answer. 
Sample Input 
5 3 
1 2 3 4 5 
1 1 3 
2 5 0 
1 4 5 
 
### Sample Output 
10 
8 

## 翻译
```
  Ryuji不是一个好学生，他不想学习。 但他应该学习n本书，每本书都有自己的知识[i]。 不幸的是，他学的越久，得到的就越少。
   这意味着，如果他从l到r读书，他将获得a[l] * L + a [l + 1] *（L-1）+ ... + a [r1] * 2 + a [r]（L 是[l，r]的长度，等于r-l + 1）。 现在Ryuji有q问题.
   你应该回答他： 
    1。如果问题类型是1，你应该回答他读书后会得到多少知识[l，r]
    2.如果问题类型是2，Ryuji会改变 ith书对新价值的认识。
 
输入
  第一行包含两个整数n和q（n，q <= 100000）。 
  下一行包含n个整数表示a [i]（a [i] <= 1e9） 
  然后在下一个q行中每行包含三个整数a，b，c， 
  如果a = 1，则表示问题类型为1，b ，c代表[l，r]。 
  如果a = 2，则表示问题类型为2，b，c表示Ryuji将bth book的知识更改为c。

```

这里我维护的两个数组。一个是输入的数组x，另一个是数组z。
定义数组`z[i] = x[i] * (n-i+1)（i从1开始）`
然后定义两个数组 y 和 shu。其中 y数组用于维护x，shu数组用于维护z。
这个解释一下z数组的用途，以及如何维护z数组。
题目求的是`a[l] * L + a [l + 1] *（L-1）+ ... + a [r1] * 2 + a [r]`，如果暴力求解绝对超时。所以有个z数组。
用样例来说：
输入的 1 2 3 4 5 
那么 x 数组中就是  1 2 3 4 5
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;z 数组中就是 5 8 9 8 5
求 1~3 的和。那么如果直接加上 z[1~3] ，那么就是a[1]*5 + a[2]*4 + a[3]*3。但是题目要求的是  a[1]*3+a[2]*2+a[3]*1，也就是减去2倍的(a[1]+a[2]+a[3])。而这个2倍其实就是 区间 （l，r）中r距离尾部的单位值。这里是5 - 3 = 2。
上面的例子很容易发现 z 数组的用途，提前预处理了题目要求的`a[l] * L + a [l + 1] *（L-1）+ ... + a [r1] * 2 + a [r]`。如此一来就可以用0（1）的时间求出要求的值，而不需要遍历。
再来看，题目有两种状态一个是区间求和，另一个是修改值。碰到这种题目很容易想到的就是树状数组或者线段树，我这里用的是树状数组。
```
#include <cstdio>
#include <iostream>
using namespace std;
const int sm = 400000+10;
long long int x[sm];
long long int n, q;
long long int z[sm];// x存n个数，z ai*(n-i) i 从0 开始 
long long int y[sm], shu[sm];// y 求区间和， 树状数组

long long int lowbit(int x){
	return x&(-x);
}

long long find_sum(long long int i, long long zu[]){//区间求和 
	long long int ret =0 ;
	for(; i>0 ; ret += zu[i], i -= lowbit(i));
	return ret;
}

void update(long long int i, long long int val, long long zu[]){//建树, 更新值 
	for(;i <= n; zu[i] += val, i += lowbit(i));
}

int main() {
	cin >> n >> q;
	for(int i =1 ; i<=n; i++)
		cin >> x[i];
	for(int i=1; i<=n; i++)
		update(i, x[i], y);//建立y，维护x数组
	for(int i=1; i<=n; i++)
		z[i] = x[i] * (n-i+1);
	for(int i=1; i<=n; i++)
		update(i, z[i], shu);//建立shu，维护z数组
		
	for(int i=1; i<=q; i++)
	{
		long long int t;
		cin >> t;
		if(t == 1){
			long long int l, r, suml, sumr;
			cin >> l >> r;
			long long int s1 = find_sum(r, shu) - find_sum(l-1, shu);//获得z数组的区间和
			long long int s2 = find_sum(r, y) - find_sum(l-1, y);//获取x数组的区间和
			cout << s1 - s2*(n-r) << endl;
		}
		if(t == 2){
			long long int new_num, where;
			cin >> where >> new_num;//where代表位置，new_num代表值
			long long int mid = new_num - x[where]; 
			update(where, mid, y);//更新y数组
			update(where, mid*(n - where + 1), shu);//更新shu数组
			x[where] = new_num;//更新x数组中的值
		}
	}
    return 0;
}
```
`！！！！着重强调，如果用我这种方法做的人，一定要用``long long`` ！！！！`
本来觉得部分数据不大可以部分不用long long，结果不知道那块就是卡住了死交不过去，wa了四五发都是因为这个。


ACM本就是逆天而行，死在路上很正常。真的，看到别人大佬一队AK了，我才做了两题，就感觉对不起队友，对不起老师。天赋上的差距没办法，自己还是很菜，再加上最近在搭建服务器，导致算法上面没用心，最后一年了，好好搞。
