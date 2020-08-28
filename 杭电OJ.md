### 1003 Max Sum

**Problem Description**\
Given a sequence a[1],a[2],a[3]......a[n], your job is to calculate the max sum of a sub-sequence. For example, given (6,-1,5,4,-7), the max sum in this sequence is 6 + (-1) + 5 + 4 = 14.

**Input**\
The first line of the input contains an integer T(1<=T<=20) which means the number of test cases. Then T lines follow, each line starts with a number N(1<=N<=100000), then N integers followed(all the integers are between -1000 and 1000).
 
**Output**\
For each test case, you should output two lines. The first line is "Case #:", # means the number of the test case. The second line contains three integers, the Max Sum in the sequence, the start position of the sub-sequence, the end position of the sub-sequence. If there are more than one result, output the first one. Output a blank line between two cases.
 
**Sample Input**\
2\
5 6 -1 5 4 -7\
7 0 6 -1 1 -6 7 -5
 
**Sample Output**\
Case 1:\
14 1 4

Case 2:\
7 1 6

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
	int i, j, T, n;     //T为测试数据组数，n为数组的长度
	int *a;             //数组采用动态分布
	int l, r, x, sum, max;      //l为max的起始位置，r为max的结束位置，max为最大和
	                            //x记录sum的起始位置（由于不知道和max相比的大小，所以先另存起来）
	scanf("%d", &T);	
	for (i=1;i<=T;++i)
	{
		scanf("%d", &n);
		a=(int *) calloc (n, sizeof(int));
		for (j=1;j<=n;++j)
			scanf("%d", a+j);
		
		sum=max=a[i];
		l=r=x=1;
		for (j=2;j<=n;++j)
		{
			if (sum+a[j]<a[j])
			{
				sum=a[j];
				x=j;
			}
			else
				sum+=a[j];
			if (sum>max)
			{
				max=sum;l=x;r=j;
			}
		}
		printf("Case %d\n", i);
		printf("%d %d %d\n", max, l, r);
	}
	free (a);
	
	return 0;
}
```
### 1004 Let the Balloon Rise

**Problem Description** \
Contest time again! How excited it is to see balloons floating around. But to tell you a secret, the judges' favorite time is guessing the most popular problem. When the contest is over, they will count the balloons of each color and find the result.

This year, they decide to leave this lovely job to you.
 
**Input** \
Input contains multiple test cases. Each test case starts with a number N (0 < N <= 1000) -- the total number of balloons distributed. The next N lines contain one color each. The color of a balloon is a string of up to 15 lower-case letters.

A test case with N = 0 terminates the input and this test case is not to be processed.
 
**Output**\
For each case, print the color of balloon for the most popular problem on a single line. It is guaranteed that there is a unique solution for each test case.
 
**Sample Input**\
5\
green\
red\
blue\
red\
red\
3\
pink\
orange\
pink\
0\
 
**Sample Output**\
red\
pink\

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
struct st
{
	int count;
	char s[16];
};

int main()
{
	int i, j=0, k, n, flag;
	int max, index;
	char w[16];
	while (scanf("%d", &n)) {
		if (n==0)
			break;
		struct st a[1000];
		for (i=0;i<n;++i)
			a[i].count=0;
		for (i=0;i<n;++i){
			flag=0;
			scanf("%s", w);
			for (k=0;k<j;++k) {
				if (strcmp(a[k].s, w)==0) {
					a[k].count++;
					flag=1;
					break;
				}
			}
			if (flag==0) {
				strcpy(a[j].s, w);
				a[j].count++;
				j++;
			}
		}
		max=a[0].count;
		for (i=0;i<j;i++) {
			if (a[i].count>max) {
				max=a[i].count;
				index=i;
			}
		}
		printf("%s\n", a[index].s);
	}
	return 0;
}
```
