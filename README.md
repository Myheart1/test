# test
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
int c_char(FILE *fp)
{
	int num = 0;
	char s[20];
	while (!feof(fp))
	{
		fscanf(fp, "%s", s); //读取字符串
		num += strlen(s); //叠加字符数
	}
	printf("字符数（不计空格和回车）有%d个\n", num);
	rewind(fp); //绕回文件指针
	return num;
}
int w_world(FILE *fp)
{
	char s[20];
	int n = 0, num = 0,len=0,i=0;
	while (!feof(fp))
	{	
		len=strlen(s);
		
		if (fscanf(fp, "%s", s) && !(s[0] >= '0' && s[0] <= '9' )&&((s[0] >= 'A' && s[0] <= 'Z')||(s[0] >= 'a' && s[0] <= 'z')))
			n++;
		
		
	}
	printf("单词数有%d个\n", n);
	rewind(fp);
	return n;
}
int l_line(FILE *fp)
{
	
	int n = 1;
	char ch;
	while (!feof(fp))
	{
		if ((ch = fgetc(fp) == '\n'))
			n++;
	}
	
	rewind(fp);
	return n;
}

int e_line(FILE *fp)
{
	int len=0,i=0,signline=0;
	char s[20];
	while(!feof(fp))
	{
		fscanf(fp, "%s", s);
		
		len=strlen(s); 
		
		
		for(i=0;i<len;i++)
		{
			if((s[i]=='/'&&s[i+1]=='/')||(s[i]=='/'&&s[i+1]=='*'))
			{
				signline++;
				
				
				
				
			}
			
			
			
		}
	}
	
	
	
	
	
	rewind(fp);
	return signline;
	
}

int k_line(FILE *fp)
{
	int len=0,i=0;
	char s[20];
	int keyline=0;
	while(!feof(fp))
	{
		fgets(s,sizeof(s),fp);
		len=strlen(s);
		if(len>1)
		{
			for(i=0;i<len;i++)
			{
				if((s[i]!='/'&&s[i+1]!='/')||(s[i]!='/'&&s[i+1]!='*'))
				{
					keyline++;
				}
				break;
			}
		}
	}
	rewind(fp);
	
	return keyline;
}
void main()
{
	FILE *fp;
	int emptyline=0;
	fp = fopen("1.txt", "r"); //打开文件
	c_char(fp);
	w_world(fp);
	printf("有%d行\n", l_line(fp));
	printf("有%d注释行\n", 	e_line(fp)); 	
	printf("有%d代码行\n", 	k_line(fp)); 
	emptyline=l_line(fp)-e_line(fp)-k_line(fp);
				printf("有%d空行\n", emptyline);
				fclose(fp);
}
