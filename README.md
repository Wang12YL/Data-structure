# Data-structure
learning in C language
#include<stdio.h>
#include<stdlib.h>
#include<malloc.h>
//定义链表节点
typedef struct node{
	int number;
	struct node *pNext;
}Node,*pNode;
//函数声明 链表函数 遍历链表函数
pNode CreateList();       
void TraverList(pNode);
int Insert_Node(pNode, int, int);
int Del_Node(pNode, int);
int main()
{
	pNode pHead = NULL;
	int data, num, choose, return_val;
	pHead = CreateList();
	printf("你输入的数据是");
	TraverList(pHead);
	printf("是否进行如下操作:\n");
	printf("1、插入数据2、删除数据");
	printf("请输入：");
	scanf_s("%d", &choose);
	switch (choose)
	{
	case 1:
	{
		printf("请输入与要在第几个节点前加入数据");
		scanf_s("%d", &num);
		printf("请输入要输入的数据");
		scanf_s("%d", &data);
		if (Insert_Node(pHead, num, data) == 1)
		{
			printf("插入成功\n插入后的数据是\n");
			TraverList(pHead);
		}
		else
		{
			printf("插入失败\n");
		}
		printf("操作完成后的数据是：");
		TraverList(pHead);
		break;
	}
	case 2:
	{
		printf("请输入要删除第几个节点的数据");
		scanf_s("%d", &num);
		return_val = Del_Node(pHead, num);
		if (return_val == 0)
		{
			printf("删除失败\n");
		}
		else
		{
			printf("删除成功，删除的元素是%d\n", return_val);
		}
		printf("操作完成后的数据是");
		TraverList(pHead);
	}
	
	}
	getchar();
	getchar();
	return 0;
}
//创建链表函数
pNode CreateList()
{
	int i;
	int len;
	int val;    //存放用户输入的数据
	pNode pHead = (pNode)malloc(sizeof(Node));
	pNode pTail = pHead;    //尾节点
	pTail->pNext = NULL;
	printf("请输入节点个数");
	scanf_s("%d", &len);
	for (i = 0; i < len; i++)
	{
		printf("第%d个节点的数值:", i + 1);
		scanf_s("%d", &val);
		pNode pNew = (pNode)malloc(sizeof(Node));
		pNew->number = val;
		pTail->pNext = pNew;
		pNew->pNext = NULL;
		pTail = pNew;
	}
	return pHead;
}
//遍历链表函数
void TraverList(pNode pHead)
{
	pNode p = pHead->pNext;
	while (p!=NULL)
	{
		printf("%d ", p->number);
		p = p->pNext;
	}
	printf("\n");
	
}
//链表节点插入函数
int Insert_Node(pNode pHead, int front, int data)
{
	int i = 0;
	pNode _node = pHead;
	pNode pSwap;
	if ((front < 1) && (NULL != _node))
	{
		return 0;
	}
	while (i < front - 1)
	{
		_node = _node->pNext;
		++i;
	}
	pNode PNew = (pNode)malloc(sizeof(Node));
	PNew->number = data;
	pSwap = _node->pNext;   //插入的那个位置的后一个节点的地址给了swap 腾出来存储新的节点
	_node->pNext = PNew;
	PNew->pNext = pSwap;
	return 1;
}
int Del_Node(pNode pHead, int back)
{
	int i = 0;
	int data;
	pNode _node = pHead;
	pNode pSwap;
	if ((back < 1) && (NULL == _node->pNext))
	{
		printf("删除失败\n");
		return 0;
	}
	while (i < back - 1)
	{
		_node = _node->pNext;
		++i;
	}
	pSwap = _node->pNext;
	data = pSwap->number;
	_node->pNext = _node->pNext->pNext;
	free(pSwap);
	return data;
}
