---
profileName: Estruswent
postId: "2367"
postType: post
categories:
  - 40
---
# 一、插入排序(insertion sort)

类比打斗地主时一把摸起来的大堆扑克牌，排序方式差不多。

## （伪）代码实现
```C
void InsertionSort ( ElementType A[ ], int N ) {
	int  j, P;
	ElementType  Tmp;
	for ( P = 1; P < N; P++ ) {
		Tmp = A[ P ];  /* the next coming card */
		for ( j = P; j > 0 && A[ j - 1 ] > Tmp; j -- )
	        A[ j ] = A[ j - 1 ];
        /* shift sorted cards to provide a position for the new coming card */
		A[ j ] = Tmp;  /* place the new card at the proper position */
     }  /* end for-P-loop */

}
```
## 复杂度分析

### 时间复杂度

最好情况：已经排好了！$O(N)$
最坏情况：完全反转的。$O(N^2)$
一般情况：$O(I + N)$，I表示反转(inversion)的数有多少对。
反转：序号大而对应数据小。比如34, 8, 64, 51, 32, 21有9对反转，分别为
(34, 8) (34, 32) (34, 21) (64, 51) (64, 32) (64, 21) (51, 32) (51, 21) (32, 21)

### 空间复杂度

$O(1)$

## 稳定性分析

不改变其他序列，所以是稳定的

# 二、希尔排序(shell sort)

## 代码实现
```C
void shellSort(int arr[], int n) { 
	// 为了找到最大的希尔排序间隔，先将其初始化为数组长度
	int gap = sizeof(arr) / sizeof(arr[0])
	//进行希尔排序
	while (gap > 0) { 
		gap /= 2;
		for (int i = gap; i < n; i ++) { 
			int temp = arr[i]; int j; 
			for (j = i; j >= gap && arr[j - gap] > temp; j -= gap) { 
				arr[j] = arr[j - gap]; 
			} 
			arr[j] = temp; 
		}
	}
}
```
## 复杂度分析

### 时间复杂度
时间复杂度为$O(N^{1.5})$，时间复杂度的下界为$O(N*logN)$，上界（最坏）为$\Theta (N^2)$。

### 空间复杂度

$O(1)$

## 稳定性分析

不稳定的

# 三、堆排序(heapsort)
[Heap sort visualization | What is heap sort and How does it work?? - YouTube](https://www.youtube.com/watch?v=mgUiY8CVDhU)该视频的图解很清晰

## 代码实现
 ```C
 void heapify(int arr[], int n, int i) {
    int largest = i; // Initialize largest as root
    int left = 2 * i + 1; // left = 2*i + 1
    int right = 2 * i + 2; // right = 2*i + 2

    // If left child is larger than root

    if (left < n && arr[left] > arr[largest])
        largest = left;

    // If right child is larger than largest so far

    if (right < n && arr[right] > arr[largest])
        largest = right;

    // If largest is not root

    if (largest != i) {
        int swap = arr[i];
        arr[i] = arr[largest];
        arr[largest] = swap;
        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
} 

// Main function to do heap sort

void heapSort(int arr[], int n) {
    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i --)
        heapify(arr, n, i);
    // One by one extract an element from heap
    for (int i = n - 1; i >= 0; i --) {
        // Move current root to end
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;
        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }

}
```

## 复杂度分析

### 时间复杂度

- 建立堆的时间复杂度是 $O(n)$，其中n是数组的长度。
- 调整堆的时间复杂度是 $O(\log n)$，因为每次调整堆的操作只会影响一条分支。
- 因为有n个元素需要被移除并调整堆，所以总的时间复杂度是 $O(n \log n)$。

### 空间复杂度

不需要额外空间，仅为$O(1)$

## 稳定性分析

不稳定的

# 四、归并排序

## 代码实现

```C
void merge(int arr[], int l, int m, int r) { 
	int i, j, k; 
	int n1 = m - l + 1; 
	int n2 = r - m; 
	// 创建临时数组 
	int L[n1], R[n2]; 
	// 拷贝数据到临时数组 
	for (i = 0; i < n1; i++) 
		L[i] = arr[l + i]; 
	for (j = 0; j < n2; j++) 
		R[j] = arr[m + 1 + j]; 
	
	// 合并临时数组回到原数组 
	i = 0; 
	j = 0; 
	k = l; 
	while (i < n1 && j < n2) { 
		if (L[i] <= R[j]) { 
		arr[k] = L[i]; i++; 
		} else { 
		arr[k] = R[j]; j++; 
		} 
		k++; 
	} 
	// 拷贝 L[] 的剩余元素 
	while (i < n1) { 
	arr[k] = L[i]; 
	i++; 
	k++; 
	}
	// 拷贝 R[] 的剩余元素 
	while (j < n2) { 
	arr[k] = R[j]; 
	j++; 
	k++; 
	} 
} 


// 主函数用于排序 
void mergeSort(int arr[], int l, int r) { 
	if (l < r) { 
		// 找到中间点 
		int m = l + (r - l) / 2; 
		// 分别对前半部分和后半部分进行排序 
		mergeSort(arr, l, m); 
		mergeSort(arr, m + 1, r); 
		// 合并两个有序部分 
		merge(arr, l, m, r); 
	} 
}
```

## 复杂度分析

### 时间复杂度

$O(N \log N)$

### 空间复杂度

需要总共长度为N的若干数组，故空间复杂度为$O(N)$

## 稳定性分析

稳定的（它不会改变相等元素的排序）