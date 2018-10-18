//# -
//like 扫雷一样
// ConsoleApplication2.cpp : 此文件包含 "main" 函数。程序执行将在此处开始并结束。
//
#include "pch.h"
#include<iostream>
#include<string>
#include<stdio.h>
#include<string.h> 
#include<stdlib.h>
#include<ctime>
//定义10*10但是只要9*9  有10个雷
//数字0-8为未揭晓的的无雷|9 表示有雷未揭晓 |10-18表示无雷已揭晓|19表示有雷已经揭晓
int s[18][18];
void ti(int a, int b)//0的显示函数
{
	s[a][b] = s[a][b] + 10;
	if (s[a + 1][b] ==0&&(a+1)!=17)ti(a + 1, b);
	if (s[a - 1][b] ==0 && (a - 1) != 0)ti(a - 1, b);
	if (s[a][b + 1] ==0 && (b + 1) != 17)ti(a, b + 1);
	if (s[a][b - 1] ==0 && (b- 1) != 0)ti(a, b - 1);
}
int main()
{
	printf("欢迎来到由李泽浩制作的扫雷小游戏！\n\n");
	printf("这是中级难度，16*16个格子共计十个雷\n\n");
	printf("请先输入一个数字，表示横着的行号，按下回车\n\n");
	printf("再输入一个数字，表示竖着的列号，按下回车\n\n");
	printf("然后不断循环，直到找完所有雷，全屏体验更佳哦！\n\n");
	srand(time(NULL));
	memset(s, 0, sizeof(s));
	for (int i = 1; i <= 40 ;i++)
	{
		int a = (rand() % 16);
		if (a == 0)a = 1;
		int b = (rand() % 16);
		if (b == 0)b = 16;
		s[a][b] = 9;
	}//生成40个雷
	for (int a = 1; a <= 16; a++) 
	{
		for (int b = 1; b <= 16; b++)
		{
			if (s[a][b] == 9) 
			{    
				if (s[a][b - 1] !=9)s[a][b - 1] ++;
				if (s[a][b + 1]!= 9)s[a ][b + 1] ++;
				if (s[a - 1][b-1] != 9)s[a - 1][b-1] ++; 
				if (s[a - 1][b] != 9)s[a - 1][b] ++;
				if (s[a - 1][b + 1] != 9)s[a - 1][b + 1] ++; 
				if (s[a + 1][b - 1] != 9)s[a + 1][b - 1] ++;
				if (s[a + 1][b + 1] != 9)s[a + 1][b + 1] ++;
				if (s[a + 1][b ] != 9)s[a + 1][b ] ++;
			}
			else continue;
		}
	}//生成周围雷数
	for (int a = 1; a <= 16; a++) 
	{
		for (int b = 1; b <= 16; b++)
		{
			if (s[a][b] < 10)
				printf(" ?  ");
			else if (s[a][b] == 9) 
			{
				printf("你踩中雷了哈哈哈");
				for (a = 1; a <= 9; a++) 
				{
					for (b = 1; b <= 9; b++)
					{
						if (s[a][b] == 9)printf(" 雷 ");
						else printf(" %d  ", s[a][b] % 10);
					}
					printf("\n\n");
			     }
			

			}
			else printf(" %d   ", s[a][b]);
		}
		printf("\n\n");
	}
	int a, b;
	printf("请输入行 ,回车;再输入列，然后再回车：\n");
	while (scanf("%d%d", &a, &b) == 2)
	{
		printf("\n");
		if (a > 16 || a < 1 || b>16 || b < 1)continue;
		else if (s[a][b] > 9)continue;
		else if (s[a][b] == 9)
		{
			printf("\n你踩中雷了哈哈哈\n\n");
			for (a = 1; a <= 16; a++)
			{
				for (b = 1; b <= 16; b++)
				{
					if (s[a][b] == 9)printf(" 雷 ");
					else printf(" %d  ", s[a][b] % 10);
				}
				printf("\n\n");
			}
			break;
		}
		else if (s[a][b] < 9 && s[a][b] != 0)s[a][b] = s[a][b] + 10;//没雷 大于零
		else if (s[a][b] == 0)
		{
			ti(a, b);
			for (a = 1; a <= 16; a++)
			{
				for (b = 1; b <= 16; b++)
					if (s[a][b] == 10)
					{
						if (s[a][b - 1] < 9)s[a][b - 1] += 10;
						if (s[a][b + 1] < 9)s[a][b + 1] += 10;
						if (s[a - 1][b - 1] < 9)s[a - 1][b - 1] += 10;
						if (s[a - 1][b] < 9)s[a - 1][b] += 10;
						if (s[a - 1][b + 1] < 9)s[a - 1][b + 1] += 10;
						if (s[a + 1][b - 1] < 9)s[a + 1][b - 1] += 10;
						if (s[a + 1][b + 1] < 9)s[a + 1][b + 1] += 10;
						if (s[a + 1][b] < 9)s[a + 1][b] += 10;
					}
			}
		}
		//数字0-8为未揭晓的的无雷|9 表示有雷未揭晓 |10-18表示无雷已揭晓|19表示有雷已经揭晓
		for (a = 1; a <= 16; a++)
		{
			for (b = 1; b <= 16; b++)
			{
				if (s[a][b] < 10)printf(" ?  ");
				else if (s[a][b] == 10)printf(" 0  ");
				else printf(" %d  ", s[a][b] % 10);
			}
			printf("\n\n");
		}
		int count = 0;
		for (a = 1; a <= 16; a++)
		{
			for (b = 1; b <= 16; b++)
				if (s[a][b] <= 9)count++;

		}
		printf("请输入行 ,回车;再输入列，然后再回车：\n");
		if (count == 40) {
			printf("恭喜你赢了！");
			break;
		}
	}
	system("pause");
	return 0;
}

