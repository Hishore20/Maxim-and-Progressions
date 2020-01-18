# Maxim-and-Progressions

/*

Maxim likes arithmetic progressions and does not like sequences which are not arithmetic progressions.

Now he is interested in the question: how many subsequences of his sequence a, consisting of n elements, are not arithmetic progressions.

Sequence s[1],s[2],...,s[k] is called a subsequence of sequence a[1],a[2],...,a[n], if there will be such increasing sequence of indices i[1],i[2],...,i[k] (1<=i[1]<i[2]<... <i[k]<=n), that a[i[j]]=s[j]. In other words, sequence s can be obtained from the a by deleting some elements.

Sequence s[1],s[2],...,s[k] is called an arithmetic progression, if it can be represented as :

s[1]=p, where p some integer;
s[i]=p+(i-1)q (i>1), where q some integer.
In particular, the empty sequence or a sequence of one element is an arithmetic progression.



Input

The first line of the input contains an integer T denoting the number of test cases. The description of T test cases follows.

The first line of each test case contains an integer n the number of elements in the sequence. The next line of the test case contains n integer, a[1],a[2],...,a[n] elements of the sequence.

Output

For each test case print the remainder of the division the answer on 1000000007 (10^9+7). All answers print on different lines.

Constraints

1<=T<=10

1<=n<=200000

1<=a[i]<=100
Logic Test Case 1

Input (stdin)
2

1

1

3

1 2 1

Expected Output

0

1
Logic Test Case 2

Input (stdin)
1

4

1 5 6 2

Expected Output

5

*/



#include <stdio.h>
#include<stdlib.h>
#include<math.h>
#define mod 1000000007L
long long int p[200001];
int a[200001];
int main()
{
    long long int dp1[101][101],dp2[101][101],dp3[101];
    long long int count[101],res,gen;
    int i,j,k,t,n,temp;
    p[0]=0;
    for(i=1;i<=200000;i++)
    {
        p[i]=((p[i-1]+1)*2)-1;
        p[i]=p[i]%mod;
    }
    scanf("%d",&t);
    while(t--)
    {
        res=0;
        scanf("%d",&n);
        for(i=0;i<=100;i++)
        {
            count[i]=0;
            dp3[i]=0;
            for(j=0;j<=100;j++)
            {
                dp1[i][j]=0;
                dp2[i][j]=0;
            }
        }
        for(i=0;i<n;i++)
            scanf("%d",&a[i]);
        for(i=n-1;i>=0;i--)
        {
            temp=a[i];
            for(k=0;k<=100;k++)
            {
                if(k==0)
                {
                    count[temp]++;
                    dp3[temp]=p[count[temp]];
                }
                else
                {
                    if(temp+k<=100)
                    {
                        dp2[temp][k]+=count[temp+k]+dp2[temp+k][k];                            dp2[temp][k]=dp2[temp][k]%mod;
                    }
                    if(temp-k>0)
                    {
                        dp1[temp][k]+=count[temp-k]+dp1[temp-k][k];                            dp1[temp][k]=dp1[temp][k]%mod;
                    }
                }
            }
        }
        for(i=0;i<=100;i++)
        {
            res+=dp3[i];
            for(j=0;j<=100;j++)
            {
                res+=dp1[i][j]+dp2[i][j];
                res=res%mod;
            }
        }
        gen=(p[n]-res)+mod;
        gen=gen%mod;
        printf("%lld\n",gen);
    }
    return 0;
}
