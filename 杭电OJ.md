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
