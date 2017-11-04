# Crazy-Search

Crazy Search

Description

Many people like to solve hard puzzles some of which may lead them to madness. One such puzzle could be finding a hidden prime number in a given text. Such number could be the number of different substrings of a given size that exist in the text. As you soon will discover, you really need the help of a computer and a good algorithm to solve such a puzzle.

Your task is to write a program that given the size, N, of the substring, the number of different characters that may occur in the text, NC, and the text itself, determines the number of different substrings of size N that appear in the text.


As an example, consider N=3, NC=4 and the text "daababac". The different substrings of size 3 that can be found in this text are: "daa"; "aab"; "aba"; "bab"; "bac". Therefore, the answer should be 5.


Input

The first line of input consists of two numbers, N and NC, separated by exactly one space. This is followed by the text where the search takes place. You may assume that the maximum number of substrings formed by the possible set of characters does not exceed 16 Millions.

Output

The program should output just an integer corresponding to the number of different substrings of size N found in the given text.

Sample Input

3 4

daababac

Sample Output

5

Hint

Huge input,scanf is recommended.

这个是说一段字符串 有nc种字符组成 问长度为n的不同的字符串有多少个
非常关键的一条信息是 nc^n最多只有16 000 000
so 我们用nc进制的HASH来做


#include <stdio.h>

#include <string.h>

int n,nc;

char str[20000000];

char asca[128];

int hash[16000005];


int main()

{

    while(scanf("%d%d\n",&n,&nc)!=EOF)
    
    {
    
        scanf("%s",str);
        
        int i=0;
        
        int j;
        
        int key=0;
        
        while(str[i])
        
        {
        
            if(asca[str[i]]==0) asca[str[i]]=++key;
            
            i++;
            
            if(key==nc) break;
            
        }
        
        int len=strlen(str);
        
        int sum;
        
        int cnt=0;
        

        for(i=0;i+n-1<len;i++)
        
        {
        
            sum=0;
            
            for(j=i;j<=i+n-1;j++)
            
            {
            
            sum=sum*nc+asca[str[j]]-1;
            
            }
            
            if(hash[sum]==0) 
            
            {
            
                hash[sum]=1;
                
                cnt++;
                
            }
            
        }
        

        printf("%d\n",cnt);
        

    }
    
}
