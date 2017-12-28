#include<stdio.h>
#include<stdlib.h>
#include<time.h>

#define blank ' '
#define wall '*'
#define food '$'
#define head 'H'
#define body 'X'
#define maxlength 99

void printer(void);//游戏界面打印
void move(int x, int y);//蛇动作实现。x在-1，1，0时分别表示左走，右走，不走；y在-1，1，0时分别表示下走，上走，不走
void refresh(void);//更新地图情况
void creatfood(void);//随机生成食物

int locationx[maxlength] = { 1,1,1,1,1 },
locationy[maxlength] = { 1,2,3,4,5 };//定义数组存储蛇躯体在地图上坐标
int length = 5;//储存蛇当前长度
int lastx, lasty;//储存蛇尾原坐标
int foodx, foody;//储存食物坐标

int map[12][12] = { { -1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1 },
{ -1,1,1,1,1,2,0,0,0,0,0,-1 },
{ -1,0,0,0,0,0,0,0,0,0,0,-1 },
{ -1,0,0,0,0,0,0,0,0,0,0,-1 },
{ -1,0,0,0,0,0,0,0,0,0,0,-1 },
{ -1,0,0,0,0,0,0,0,0,0,0,-1 },
{ -1,0,0,0,0,0,0,0,0,0,0,-1 },
{ -1,0,0,0,0,0,0,0,0,0,0,-1 },
{ -1,0,0,0,0,0,0,0,0,0,0,-1 },
{ -1,0,0,0,0,0,0,0,0,0,0,-1 },
{ -1,0,0,0,0,0,0,0,0,0,0,-1 },
{ -1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1 } };
//地图：-1为障碍，0为空，1为蛇身，2为蛇头，3为食物

int flag = 1;//表示游戏状态。1表示可以继续，0表示游戏结束

int main(void)
{
	char kbi, lastmove = 'D';
	srand(time(NULL));
	creatfood();
	printer();
	while (flag)
	{
		kbi = getch();
		switch (kbi)
		{
		case 'A':
			if (lastmove == 'D') break;
			else move(-1, 0);
			lastmove = kbi;
			break;
		case 'S':
			if (lastmove == 'W') break;
			else move(0, -1);
			lastmove = kbi;
			break;
		case 'D':
			if (lastmove == 'A') break;
			else move(1, 0);
			lastmove = kbi;
			break;
		case 'W':
			if (lastmove == 'S') break;
			else move(0, 1);
			lastmove = kbi;
			break;
		}
		system("cls");
		printer();
	}
	system("cls");
	printf("************\n*          *\n*          *\n*          *\n*          *\n*   GAME   *\n*   OVER   *\n*          *\n*          *\n*          *\n*          *\n************\n");
	return 0;
}

void printer(void)
{
	for (int i = 0; i < 12; i++)
	{
		for (int j = 0; j < 12; j++)
		{
			switch (map[i][j])
			{
			case -1:printf("%c", wall); break;
			case 0:printf("%c", blank); break;
			case 1:printf("%c", body); break;
			case 2:printf("%c", head); break;
			case 3:printf("%c", food); break;
			defult:break;
			}
			
		}
		if (i == 5) printf("     Welcome To Snake Game!");
		if (i == 6) printf("     Use W S A D to control");
		printf("\n");
	}
}

void move(int x, int y)
{
	lastx = locationx[0];
	lasty = locationy[0];
	if (x == 1)
	{
		for (int i = 0; i < length - 1; i++) locationy[i] = locationy[i + 1];
		locationy[length - 1]++;
	}
	else if (x == -1)
	{
		for (int i = 0; i < length - 1; i++) locationy[i] = locationy[i + 1];
		locationy[length - 1]--;
	}
	else if (x == 0) for (int i = 0; i < length - 1; i++) locationy[i] = locationy[i + 1];
	if (y == 1)
	{
		for (int i = 0; i < length - 1; i++) locationx[i] = locationx[i + 1];
		locationx[length - 1]--;
	}
	else if (y == -1)
	{
		for (int i = 0; i < length - 1; i++) locationx[i] = locationx[i + 1];
		locationx[length - 1]++;
	}
	else if (y == 0) for (int i = 0; i < length - 1; i++) locationx[i] = locationx[i + 1];
	if ((map[locationx[length - 1]][locationy[length - 1]] == -1) || (map[locationx[length - 1]][locationy[length - 1]] == 1)) //蛇前进碰壁或蛇身
	{
		flag = 0;
		return;
	}
	if ((locationx[length - 1] == foodx) && (locationy[length - 1] == foody)) //蛇吃到食物：生成新食物，蛇长长一节
	{
		refresh(0);
		creatfood();
	}
	else refresh(1);
}

void refresh(int isgrow) //isgrow判断蛇是否吃到食物，1代表没有吃到，0代表吃到
{
	if (isgrow)
	{
		map[lastx][lasty] = 0;
		map[locationx[length - 1]][locationy[length - 1]] = 2;
		map[locationx[length - 2]][locationy[length - 2]] = 1;
	}
	else
	{
		length++;
		for (int i = length - 2; i >= 0; i--)
		{
			locationx[i] = locationx[i - 1];
			locationy[i] = locationy[i - 1];
		}
		locationx[0] = lastx;
		locationy[0] = lasty;
		locationx[length - 1] = foodx;
		locationy[length - 1] = foody;
		map[locationx[length - 1]][locationy[length - 1]] = 2;
		map[locationx[length - 2]][locationy[length - 2]] = 1;
	}
}


void creatfood(void)
{
	foodx = rand() % 10 + 1;
	foody = rand() % 10 + 1;
	if (map[foodx][foody] == 0) map[foodx][foody] = 3;
	else creatfood();
}
