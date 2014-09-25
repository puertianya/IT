IT
==

2014.9.25

//24点C++代码

#include <stdio.h>
#include <string.h>
int judge(int numbers[4],char compute[4])//判断相应的数字和符号排列是否能算出24
{ 
	int result = numbers[0]; 
	int i; for(i = 0;i < 3;i++) 
	{  
		switch(compute[i]) 
	{   
	    case '+':   
	{  
		result = result + numbers[i+1];  
	break;  
	}   case '-':  
	{  
		result = result - numbers[i+1];  
		break; 
	} 
	case '*':  
	{  
		result = result * numbers[i+1];  
		break; 
	}  
	case '/': 
		{  
			if(result % numbers[i+1] == 0) 
			{   
				result = result / numbers[i+1];   
				break;  
			}  
			else return 0; 
		}  
	default:  return 0; 
		}
	} return result;
}
int twentyfour(int numbers[4])
{ int i,j,k; 
int ret=0,count=0;
char symbol[4] = {'+','-','*','/'}; 
char compute[4] = {0};
for(i = 0;i < 4;i++)
{ 
	if(numbers[i] < 1||numbers[i] > 13) 
	{  
		printf("please input correct number\n");  
		return -1; 
	}
} 
for(i = 0;i < 4;i++)
{ 
	memset(compute,0,4); 
	compute[0] = symbol[i];
	for(j = 0;j < 4;j++) 
	{   compute[1] = symbol[j]; 
	for(k = 0;k < 4;k++) 
	{ 
		compute[2] = symbol[k]; 
		printf("");  
		if(strchr(compute,'*') == NULL&&strchr(compute,'+') == NULL)  
			continue;    ret = judge(numbers,compute);    if(ret == 24)  
		{   
			printf("((%d %c %d) %c %d) %c %d\n",numbers[0],compute[0],numbers[1],compute[1],numbers[2],compute[2],numbers[3]);  
			count ++;  
		}  
	} 
	}
} return count;
}
void perm(int per[4], int m)
{  
	int i;  
	char tmp;
	if (m < 3)
	{  
		perm(per, m + 1); 
		for (i = m + 1; i < 4; i++)
		{  
			if(per[m] != per[i])  
		{  
			tmp = per[m];  
			per[m] = per[i]; 
			per[i] = tmp;  
			perm(per, m + 1);   
			tmp = per[m];   
			per[m] = per[i];   
			per[i] = tmp;  
			} 
		}
	}else
	{ 
		twentyfour(per);
	}  
	return;
}
int main()
{
	int a[4];
	printf("请输入一个数字后按enter回车后继续输入\n");
	printf("要求每个数字大小在1-13之间\n");
	printf("input:\n");
	scanf("%d%d%d%d",a,a+1,a+2,a+3); 
	perm(a,0);
	
	return 0;
}
