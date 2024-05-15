---
profileName: Estruswent
postId: "21"
postType: post
categories:
  - 1
---
# 双向链表
## 1.定义
一般而言，我们认为双向链表的C语言定义如下：
```C
struct node{
	struct node* prev;
	int data;
	struct node* next;
}link;
```

## 2.操作
### 2.1 末尾插入

```C
struct node* AddToEnd(struct node* head,int newdata){
	struct node ptr = head;
	
	struct node* temp;
	temp = (struct node*)malloc(sizeof(struct node));
	temp->next = NULL;
	temp->data = newdata;
	
	while( ptr->next != null){
		ptr = ptr->next;
	}
	ptr->next = temp;
	temp->prev = ptr;
	return head;
}
```

### 2.2 头部插入

```C
struct node* AddToHead(struct node* head,int newdata){
	struct node* temp;
	temp = (struct node*)malloc(sizeof(struct node*));
	temp->prev = NULL;
	temp->data = newdata;
	temp->next = head;
	head->prev = temp;
	head = temp;
	return head;
}
```

### 2.3 中间插入

```C
//此处为了实现添加节点位置的确定，用“第N个节点”来进行描述，即：在第N个节点后插入新节点。
//其他情况诸如“查找第某个节点的数据”，实现方法类似。
struct node* AddToMid(struct node* head, int newdata, int N){
	struct node* ptr = head;
	struct node* temp;
	temp = (struct node*)malloc(sizeof(struct node*));
	temp->prev = NULL;
	temp->next = NULL;
	temp->data = newdata;
	
	for(int i = 1;i < N;i ++){
		ptr = ptr->next;
	}

	temp->next = ptr->next;
	(ptr->next)->prev = temp;//step 1
	
	temp->prev = ptr;
	ptr->next = temp;//step 2

	return head;
}
```

### 2.4 创建双链表

```C
//此处假定已给出头节点
struct node* createlinklist(struct node* head){
	printf("请输入节点个数:\n");
	scanf("%d", &N);
	if(N == 0){
		head = NULL;
		return head;
	}

	int newdata, i;
	//创建第一个节点，情况特殊，所以单独处理。
		printf("请输入第1个节点的数据：\n");
		scanf("%d", &newdata);
		head->prev = NULL;
		head->next = NULL;
		head->data = newdata;

	if(N > 1){
		struct node* ptr = head;
		struct node* temp;
		for(i = 2;i <= N;i ++){
			printf("请输入第%d个节点的数据：\n", i);
			scanf("%d", &newdata);
			//新节点创建
			temp = malloc(sizeof(struct node*))
			temp->next = NULL;
			temp->prev = ptr;
			temp->data = newdata;
			ptr = temp;
			free(temp);
		}
	}
	return head;
}
```

### 2.5 删除节点

```C
//此处为了实现删除节点位置的确定，用“第N个节点”来进行描述，即：删除第N个节点。
//其他情况诸如“查找第某个节点的数据来确定删除节点”，实现方法类似。
struct node* Delete(struct node* head, int N){
	struct node* ptr = head, *temp;
	for(i = 1;i < N - 1;i ++){
		ptr = ptr->next;
	}

	temp = ptr->next;//正确操作的话，删除的节点后续需要释放出来，此处即为temp
	ptr->next = temp->next;
	(temp->next)->prev = ptr;
	free(temp);

	return head;
}
```