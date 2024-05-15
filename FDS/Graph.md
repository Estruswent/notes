---
profileName: Estruswent
postId: "1759"
postType: post
categories:
  - 40
---
# New Words
nonempty 非空的
vertice  顶点[pl]
vertex 顶点
adjacent 相邻的；邻近的
subgraph 子图
incident 入射
prerequisite 先决条件，前提；预备课程
predecessor 前驱
successor 后继
transitive 可传递的
dag = directed acyclic graph 有向无环图
topological

 &nbsp; &nbsp;

# Notes
## 一、图的定义
记顶点集合为V(G) ，边的集合为E(G)，图G可表示为G(V, E)。
点的个数可表示为|V|，边的个数可表示为|E|。（顶点数不可为0）
 &nbsp; &nbsp; &nbsp; &nbsp;

## 二、相关概念

 &nbsp;

### 1.有向图
$<v_i, v_j>$代表*有序*对，$v_i$记为tail，$v_j$记为head，由tail指向head。
注：$v_i \longrightarrow v_j$用英文阐述为$v_i$ is adjacent to $v_j$; $v_j$ is adjacent from $v_i$

 &nbsp;
 
### 2.无向图
$<v_i, v_j> = <v_j, v_i> ::=$同一条边。

 &nbsp;
 
### 3.简单图
1.不存在重复边。 
2.没有指向自身的边(self loop)。
注：这门课程目前应该是基本只讨论简单图，所以ppt中给出了限制。

 &nbsp;
 
### 4.多重图
概念与简单图是相反的，两节点间边数多于一条，又允许顶点用一条边和自己相连，则为多重图。

 &nbsp;
 
### 5.完全图
对有向图而言，当顶点数为n时，边数为n(n-1)，该图就为完全图。
对无向图而言，当顶点数为n时，边数为n(n-1)/2，该图就为完全图。

 &nbsp;
 
### 6.子图（subgraph）与生成子图
子图：对于两个图$G(V,  E), G_0(V_0,E_0)$ ，如果$V_0$是$V$的子集，$E_0$是$E$的子集，那么$G_0$叫做$G$的子图。
生成子图：如果上述两个图的顶点数（V）相等，那么$G_0$称为$G$的生成子图。
注：不是V和E的任何子集都能构成G的子图，因为它可能不构成图，即E的子集中的某些边关联的顶点可能不在这个V的子集中。

 &nbsp;
 
### 7.路径(path)、简单路径(simple path)与路径长度(length of a path)
路径：​顶点$v_p$到顶点$v_q$之间的一条路径是指顶点序列$\{v_p , v_{i_1} ,v_{i_2} , ... , v_{i_m} , v_q\}$，由$(v_p,v_{i_1}), (v_{i_1}, v_{i_2}),...,(v_{i_m},v_q)$或者$<v_p,v_{i_1}>, <v_{i_1}, v_{i_2}>,...,<v_{i_m},v_q>$ 构成。
简单路径：从顶点$v_i$到$v_j$的路径，顶点不能重复出现（distinct）。
路径长度：路径的边的个数。

 &nbsp;
 
### 8.回路(cycle)
回路：除了第一个和最后一个位置可以相同，其他顶点都不相同的路径，称为回路或环。
注：ppt此处定义的回路就是简单回路。

 &nbsp;
 
### 9.连通(connected)与强连通(strongly connected component)

顶点的连通：如果无向图G中两个顶点之间有路径存在，就称这两个顶点为连通。
图的连通（连通图）：如果在图中，每两个(pair of)顶点都是连通的，我们就称这个图为连通图。
连通分量(component of an undirected G)：无向图G中最大的连通子图（相当于把图分成几个部分）。
顶点的强连通：如果有向图G中两个顶点之间，存在路径$<v_i, v_j>$和$<v_j, v_i>$（也就是说，是双向的捏），那么就说这对顶点强连通。
图的强连通（强连通图）：如果在有向图G中，每两个(pair of)顶点都是强连通的，我们就称这个图为强连通图。
强连通分量(strongly connected component)：有向图G中的最大连通子图。

 &nbsp;
 
### 10.度(degree)、入度(in-degree)与出度(out-degree)

度：一个顶点的所连的边的数目(number of edges incident to...)
入度：（在有向图中）指向顶点/顶点为终点的边的数目。
出度：（在有向图中）顶点为起点的边的数目。
注：在|V|个顶点，|E|条边中的无向图中， 记每个顶点的度为K，$\sum _{i = 1}^{|V|}K_i=2|E|$

 &nbsp;
 
### 11.树(tree)与有向无环图(DAG)
树：一个连通且不成环的树。
注：同时也是包含*全部顶点*的*极小*连通子图。
有向无环图：（通俗易懂hhh）$E$中都是有方向的边且不构成回路。
&nbsp;&nbsp;
**总结：这些衍生出来的定义得记牢，英文和中文在脑子里要对应得上**
 &nbsp; &nbsp; &nbsp; &nbsp;

## 三、图的储存结构（或者表述为代表）(representation of graphs)
 &nbsp;
### 1.邻接矩阵(adjacency matrix)
思路是将$<v_i, v_j>$中$i$和$j$，通过0和1写进矩阵中（或者说二维数组？），记为：
$$
A[i][j] = \left\{\begin{matrix}
1  & 如果(v_i,v_j)或<v_i, v_j>或<v_j, v_i>为G的边 \\
0  & 如果(v_i,v_j)不为G的边
\end{matrix}\right.
$$
 &nbsp;
#### 1.1 无向图中：
性质1：对角线上全为0，且邻接矩阵关于矩阵对角线对称(symmetric)。
注：这代表着储存无向图的数据可以只存储一半左右，节省了空间(save space!)。
性质2：$v_i$构成端点所连接的边的数目可以从第$i$列或第$i$行读出，即有多少个1，就连接了多少条边。
性质3：$v_i$构成端点的邻接点可以从第$i$列或第$i$行读出，即读出结果为1的列，就为对应的邻接点下标。
 &nbsp;
#### 1.2 有向图中：
性质1：对角线上全为0，但不一定对称。
性质2：“竖入横出“，即寻找顶点$v_i$的入度，可以将其所对应的列（列是竖着排放数据的）的各项求和；寻找顶点$v_i$的出度，可以将其所对应的行（行是横着排放数据的）的各项求和。其中为1的项代表$v_i$与该顶点连通。
 &nbsp;
#### 1.3 代码实现
这个结构要记录的东西：顶点数目|V|、边数目|E|、顶点名称、邻接矩阵。
时间复杂度$O(1)$，空间复杂度$O(n^2)$。
注：缺点就是当顶点多而边少的情况下很浪费空间。

```C
#define maxsize 1007
typedef struct {
	//v和e分别代表顶点数目和边数目
	//有向图中会把边数目记作弧数，也可以用a(arcnum)代替e
	int v, e;
	char V[maxsize];//存储顶点V
	int E[maxsize][maxsize];//存储E的邻接矩阵
} amgraph;
```
 &nbsp;
### 2.邻接表(adjacency lists)
 &nbsp;
#### 2.1 概念理解
有点复杂抽象，我将其简单理解为多个链表的头指针”放“在一个数组里，而这个数组和其他要素一同组成了邻接表结构。
注1：更适用于稀疏图的存储，也就是上述”顶点多边少“的情况。
注2：”放“的是链表而非数组的原因是方便后续添加新的边。

所以嘞......话不多说，上代码！
 &nbsp;
#### 2.2 基本定义
```C
//邻接表每个节点存储表示
struct edgenode {
	int index;//顶点的位置（理解成标记，所以不一定是int）
	struct node* next;//指向下一节点的指针
} edgenode;

//邻接表的存储结构
struct algraph {
	int v, e;//顶点和边的数量
	struct node **adjlist;//二维指针
} algraph;
```
 &nbsp;
#### 2.3 相关操作

##### 2.3.1 创建节点
嗯，很基础，链表的基本操作......
```C
struct node *create_node(int newindex) {
	//要创建一个新节点，为其分配空间
	struct node* temp = (struct node*) malloc(sizeof(struct node));
	//赋予节点数据
	temp->index = newindex;
	temp->next = NULL;
	return temp;
}
```

##### 2.3.2 创建并初始化邻接表
其他部分比较基础，关键点在于这个二维指针的处理。
注：我们也可以把边new_e赋值为0，实现边数目的初始化（便于计算边数目的变化）。
```C
struct algraph *create_adjlist(int new_v, int new_e) {
	//为邻接表分配空间
	struct algraph *temp = malloc(sizeof(struct algraph));
	//为这个二维指针指向分配了数目为new_v（即顶点数）个空间，
	//而每个空间都是struct node*的大小。
	//此处使用calloc函数让其初始化。
	temp->adjlist = calloc(new_v, sizeof(struct node*));
	//其他数据
	temp->v = new_v;
	temp->e = new_e;
	//初始化结束，返回邻接表的指针
	return temp;
}
```
&nbsp;
### 3.邻接多重表(adjacency multilists)
&nbsp;
#### 3.1 概念理解
邻接多重表是*无向图*的另一种链式存储结构。

&nbsp;
### 4.加权图(weighed edges)
加权图相当于给边加了一个值，边的值就不再是清一色的”1“。
对于邻接矩阵而言，相当于将矩阵中的1改为相应的权。
对于邻接表和临界多重表而言，相当于在结构体中加入了权(weight)数据，代码如下：
```C
struct edgenode {
	int index;//顶点的位置（理解成标记，所以不一定是int）
	struct node* next;//指向下一节点的指针
} edgenode;
```
&nbsp;
## 四、拓扑排序
&nbsp;
### 1.定义
&nbsp;
#### 1.1 AOV网
一个工程中的有向图，其顶点代表一些活动，而弧代表一些关系，这种有向图就叫AOV网(AOV network = Activity on Vertex Network)。
$e.g.$在三墩镇职业技术学院的计算机课程中，你需要先上”程序设计与算法基础“（记为$C_1$）这门课之后，才能上”数据结构基础“(记为$C_2$)，那么这个AOV网可以表示为：
$$
C_1 \longrightarrow C_2
$$
&nbsp;

#### 1.2 前驱(predecessor)与后继(successor)
前驱&后继：从顶点i到顶点j存在路径，i就是j的前驱，j就是i的后继。
直接前驱&直接后继：i和j之间存在弧$<i, j>$，那么i就是j的直接前驱，j就是i的直接后继。

&nbsp;

#### 1.3 偏序(partial order)
无自反性(irreflexive)且可传递(transitive)的序关系（也可以叫前驱关系）(precedence relation)叫偏序。
注1：无自反性是指*不会有顶点指向顶点自己的弧*
注2：可传递性是指$a\longrightarrow b,b\longrightarrow c\Rightarrow a\longrightarrow c$

&nbsp;

#### 1.4 拓扑序列与拓扑排序
对于一个图$G(V, E)$，如果对于V中顶点$V_i$与$V_j$，存在从$V_i$到$V_j$的路径，那么在顶点序列中，$V_i$一定在$V_j$之前，这就叫拓扑序列；
而将一个有向图构成拓扑序列，就叫拓扑排序。（拓扑序列并不一定唯一）

&nbsp;

### 2.improvement伪代码实现
用栈和队列实现记录入度为零的顶点。
而这种方法就是用栈和队列，相当于把这些顶点的序列压缩为横着的一行。
```C
void Topsort( Graph G ) {
	//定义一个队列Q，储存若干轮次筛选后入度为0的顶点
	Queue  Q;
	int  Counter = 0;
	Vertex  V, W;
	//创建Q的大小（顶点数目）
	Q = CreateQueue( NumVertex );
	//初始化Q
	MakeEmpty( Q );
	//这个循环是为了将入度为0的顶点筛入队列
	//显然,这个循环的时间复杂度为O(|V|)
	for ( each vertex V ) {
		if ( Indegree[ V ] == 0 ){
			Enqueue( V, Q );
		}
	}
	//直到顶点排完，有多少条弧就循环多少次，
	//说明这个循环的时间复杂度为O(|E|)
	while ( !IsEmpty( Q ) ) {
		//从Q中取出一个顶点V
	    V = Dequeue( Q );
	    //为顶点V分配拓扑排序的序列，counter会逐渐从0递增
	    //counter赋给这个TopNum，实际上也代表了序列
		TopNum[ V ] = ++ Counter; /* assign next */
		//分析V的后继W，若W入度为1，则减为0，入队列中
		for ( each W adjacent from V ) {
			if ( – – Indegree[ W ] == 0 ) {
				Enqueue( W, Q );
			}
		}
    }  /* end-while */
    //如果counter和Numvertex不等，说明不是DAG
    if ( Counter != NumVertex ) {
	    Error( “Graph has a cycle” );
	}
	//释放Q
    DisposeQueue( Q ); /* free memory */
}
```
这种方式的时间复杂度为$O(|V| + |E|)$，的确是之前那种方法的improvement。

  &nbsp;
  
## 五、最短路径
&nbsp;

### Dijkstra算法（带权重的图的处理）
下面这个视频让我弄懂了基本概念和思路。
[Dijkstra's Shortest Paths Algorithm for Graphs - YouTube](https://www.youtube.com/watch?v=zXfDYaahsNA)
#### 1.1 实现思路
由于是单源，所以记源顶点为S，以下为实现思路：
1. **初始化**  
   - 创建一个集合`visited`，这个是记录已经找到最短路径的节点。开始时，初始化为空的就好。  
   - 创建一个优先队列（如最小堆），将源节点加入队列。  
   -  创建一个数组`distance[i]`，用于存储从源节点到其他节点的当前已知最短距离。将`distance[S]`初始化为0；将优先队列中的顶点对应的距离，设置为源到该顶点的权重；而*除优先队列以外的其他所有节点的距离初始化为无穷大*。  
  
2. **从优先队列中取出相邻距离最小的节点**  
   - 从优先队列中取出相邻距离最小的节点`u`。（如果队列为空，则算法结束。）  
   - 将节点`u`标记为已访问（将其添加到`visited`集合中）。  
  
3. **更新未访问邻居的距离**  
   - 遍历节点`u`的所有邻居`v`：  
     - 如果`distance[v]`是无穷大或其他值：  
       - 计算通过节点`u`到达节点`v`的距离，即`new_distance = distance[u] + weight(u, v)`。 
       - 如果`new_distance`小于当前已知的`distance[v]`，则更新`distance[v]`为`new_distance`。  
       - 如果节点`v`尚未在优先队列中，或者其当前优先级高于新计算的距离，则将节点`v`（及其新距离）加入优先队列。  
  
4. **重复**  
   - 重复步骤2和3，直到优先队列为空，即所有节点都已从队列中取出并被标记为已访问。  
  
5. **结果**  
   - `distance[]`数组现在得到了从源节点到图中所有其他节点的最短距离。  

&nbsp;
注1：为了提高效率，使用优先队列（如最小堆）来存储和选择未访问的节点是非常重要的。这可以确保在每一步中，都选择当前距离最小的节点进行处理。  
注2：根据AI的说法（也就说，我还未求证这个结论の其真实性捏），Dijkstra算法的时间复杂度取决于实现和使用的数据结构。使用二叉堆实现的优先队列，时间复杂度为O((V + E)logV)，其中V是节点数，E是边数。如果使用斐波那契堆，时间复杂度可以降低到O(VlogV + E)。
注3：这个算法也是源自贪心策略捏......

#### 1.2 代码实现：
```C
#define MAX 100007
bool visited[MAX] = {false};
//源顶点S
int s;
void Dijkstra(Graph *G,int s){
	//创建优先队列
	Queue *q;
	//初始化队列
	InitQueue( q );
	int distance[MAX], i;
	//for(i = 0;i <= MAX;i ++){
		if(i != s){
			//如果不是源顶点，就赋值为“无穷大”，
			//但是无穷大显然是没法直接表示的，所以取999999
			distance[i] = 999999;
		}else{
			distance[i] = 0;
			visited[i] = true;
		}
	//}
	//w就是新邻居捏
	int w, new_distance;

	//s入队列
	EnQueue(q, s);
	visited[s] = true;
	//IsEmpty判断队列是否为空
	while( !IsEmpty(q) ){
		v = DeQueue(q);
		//FirstNeighbor(G, v):求图G中顶点v的第一个邻接点，
		//若有则返回顶点号，否则返回-1。
		//NextNeighbor(G, v, w):假设图G中顶点w是顶点v的一个邻接点，返回除w和已访问外的顶点v
		for(w = FirstNeighbor(G, v);w >= 0;w = NextNeighbor(G, v, w)){
			//calculate_distance实现两顶点间权的读取
			new_distance = calculate_distance(v, w) + distance[v];
			if(new_distance <= distance[w]){
				distance[w] = new_distance;
			}
			if(visited[w] == false) {
				visited[w] = true;
				EnQueue(w);
			}
		}
	}
}
```
&nbsp;
## 六、图的遍历
&nbsp;
### 1 广度优先搜索(BFS = breadth-first search)
&nbsp;
#### 1.1 概念理解
怎么理解这个搜索方法呢？看到有非常好的一个思路，你把各顶点当成一个球，边当作绳子，那么当你用手抓住源的时候其他球就会自然下垂，其层次结构就非常清晰了，这一方法就是将各层次遍历。
广度优先搜索是一种分层的查找过程，每向前走一步可能访问一批顶点（对应绳子所连相同高度的球），它不是一个递归的算法。为了实现逐层的访问，算法还必须借助一个辅助队列，以记忆正在访问的顶点的下一层顶点。
&nbsp;
#### 1.2 代码实现
```C
/*邻接矩阵的广度遍历算法*/
void BFSTraverse(MGraph G){
	int i, j;
	Queue Q;
	//一开始全部顶点都没被访问过，所以赋为false
	for(i = 0; i < G.numVertexes; i ++){
		visited[i] = false;
	}
	InitQueue(&Q);	//初始化一辅助用的队列
	for(i = 0; i < G.numVertexes; i++){
		//若是未访问过就设置为已访问，同时纳入队列
		if(!visited[i]){
			vivited[i] = true;	//设置当前访问过
			EnQueue(&Q, i);	//将此顶点入队列
			//若当前队列不为空
			while(!QueueEmpty(Q)){
				DeQueue(&Q, &i);	//顶点i出队列
				//FirstNeighbor(G,v):求图G中顶点v的第一个邻接点，
				//若有则返回顶点号，否则返回-1。
				//NextNeighbor(G,v,w):假设图G中顶点w是顶点v的一个邻接点，返回除w外顶点v
				for(j = FirstNeighbor(G, i); j >= 0; j = NextNeighbor(G, i, j)) {
					//检验i的所有邻接点
					if(!visited[j]){
						visited[j] = true;	//访问标记
						EnQueue(Q, j);	//顶点j入队列
					}
				}
			}
		}
	}
}
```

&nbsp;

#### 1.3 复杂度分析

空间复杂度：明显队列的空间是大头，而队列的大小只需要考虑极限情况，即|V|的情况，故空间复杂度为$O(|V|)$。
时间复杂度：对于邻接矩阵而言，第一个循环将所有顶点设置为未访问，为|V|，第二个循环主要是需要访问邻接点，显然复杂度为$O(|V|^2)$；对于邻接表而言，先是顶点设置为没有访问，为|V|，然后再查找邻接点，同时邻接点的数目实际就是该顶点的边数，所以为|E|，综上，时间复杂度为$O(|E|+|V|)$。

&nbsp;

### 2.深度优先搜索(DFS = Depth First Search)

&nbsp;

#### 2.1 概念理解
这个又怎么理解呢？你就想象成“不撞南墙不回头”，一直往下一邻接点不停深挖，当碰壁了就回到上一顶点。
DFS就是这个意思，首先访问图中某一起始顶点v，然后由v出发，访问与v邻接且未被访问的任一顶点......不断地重复，如果不能继续向下访问，就回到上一个顶点，以此类推直到访问所有节点。

&nbsp;

#### 2.2 代码实现
事实上，这个遍历方法有两种方式，分别是递归和迭代，递归更简洁更清晰，所以此处仅展示递归方法。
```C
//将记录是否被访问过的数组初始化
#define MAX 100007
bool visited[MAX] = {false};

void DFS_recursion(Graph G,int v) {
	//定义一个w作为邻接点，便于后续操作
	int w;
	//源肯定要先被访问的呐！
	visited[v] = true;

	for(w = FirstNeighbor(G, v); w >= 0; w = NextNeighbor(G, v, w)){
		if( Visited[w] = false ){
			DFS_recursion(G, w);
		}
	}
}
```
&nbsp;
#### 2.3 复杂度分析
时间复杂度：对于邻接矩阵而言，为$O(|V|^2)$；对于邻接表而言，为$O(|V| + |E|)$。
空间复杂度：$O|V|$
&nbsp;
## 七、最大流问题
&nbsp;
## 八、最小生成树
&nbsp;
### 1.Prim算法
从一个顶点出发，在保证不形成回路的前提下，每找到并添加一条最短的边，就把当前形成的连通分量当做一个整体或者一个点看待，然后重复“**从已知顶点找最短的边并添加**”的操作。这里借用了别人的代码：
```C
/*Prim算法生成最小生成树*/
void MiniSpanTree_Prim(G){
	int min, i, j, k;
	int adjvex[MAXVEX];	//保存相关顶点下标
	int lowcost[MAXVEX];	//保存相关顶点间边的权值
	lowcost[0] = 0;	//初始化第一个权值为0，即v0加入生成树
	//lowcost的值为0，在这里就是此下标的顶点已经加入生成树
	adjvex[0] = 0;	//初始化第一个顶点下标为0
	for(i=1; i<G.numVertexes; i++){
		lowcost[i] = G.arc[0][i];	//将v0顶点与之组成边的权值存入数组
		adjvex[i] = 0;	//初始化都为v0的下标
	}
	for(i=1; i<G.numVertexes; i++){
		min = INFINITY;	//初始化最下权值为∞，通常设置一个不可能的很大的数字
		j = 1; k = 0;
		//循环全部顶点
		while(j < G.numVertexes){
			//如果权值不为0且权值小于min
			if(lowcost[j] != 0 && lowcost[j] < min){
				min = lowcost[j];	//则让当前权值成为最小值
				k = j;	//将当前最小值的下标存入k
			}
			j++;
		}
		print("(%d, %d)", adjvex[k], k);	//打印当前顶点边中权值的最小边
		for(j=1; j<G.numvertexes; j++){
			//若下标为k顶点各边权值小于此前这些顶点未被加入生成树权值
			if(lowcost[j] != 0 && G.arc[k][j] < lowcost[j]){
				lowcost[j] = G.arc[k][j];	//将较小权值存入lowcost
				adjvex[j] = k;	//将下标为k的顶点存入adjvex
			}
		}
	}
}

```
&nbsp;
### 2.Kruskal算法
按**权重顺序**考虑所有边，并不考虑之前是否连通（但是不能成环对吧,,,,,,）逐步添加到生成树中，同时避免形成环路。此处借用别人代码：
```C
/*Kruskar算法生成最小生成树*/
void MiniSpanTree_Kruskal(MGraph G){
	int i, n, m;
	Edge edges[MAXEDGE];	//定义边集数组
	int parent[MAXVEX];	//定义一数组用来判断边与边是否形成环路
	/*此处省略将邻接矩阵G转化为边集数组edges并按照权由小到大排序的代码*/
	for(i=0; i<G.numVertexes; i++){
		parent[i] = 0;	//初始化数组为0
	}
	for(i=0; i<G.numVertexes; i++){
		n = Find(parent, edges[i].begin);
		m = Find(parent, edge[i],end);
		/*假如n与m不等，说明此边没有与现有生成树形成环路*/
		if(n != m){
		/*将此边的结尾顶点放入下标为起点的parent中
		表示此顶点已经在生成树集合中*/
		parent[n] = m;
		printf("(%d, %d, %d)", edges[i].begin, 
						edges[i].end, edges[i].weight);
		}
	}
}

/*查找连线顶点的尾部下标*/
int Find(int *parent, int f){
	while(parent[f] > 0){
		f = parent[f];
	}
	return f;
}
```
## 九、欧拉回路(Eulerian circuit)与欧拉路径(Eulerian path)

### 1. 定义

**欧拉回路**：在一个图中，如果存在一条路径，它恰好经过每条边一次，并且起点和终点是**同一个**顶点，那么这条路径称为欧拉回路。
**欧拉路径**/**欧拉通路**：在一个图中，如果存在一条路径，它恰好经过每条边一次，但起点和终点是**不一定相同**的两个顶点，那么这条路径称为欧拉路径。
**欧拉图**：含有欧拉回路的图是欧拉图。

### 2. 判定
 
有向图存在欧拉路径与欧拉回路的**充要条件**分别是：  
- 欧拉路径：所有点的入度等于出度 或者 存在一点出度比入度大1（起点），一点入度比出度大1（终点），其他点的入度均等于出度。
- 欧拉回路：所有点的入度等于出度。
    
无向图存在欧拉路径和欧拉回路的**充要条件**分别为：  
- 欧拉路径：恰好有两个点度是奇数，其它顶点的度都是偶数 或者 每个顶点的度都是偶数，则有欧拉路径。
注：奇数度的点一定是欧拉路径的起点和终点。
- 欧拉回路：每个顶点的度都是偶数，则有欧拉回路。