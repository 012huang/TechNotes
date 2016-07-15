
# 排序

## (直接)插入排序

原理：将数组分为**无序区**和**有序区**两个区，然后不断将无序区的第一个元素按大小顺序插入到有序区中去，最终将所有无序区元素都移动到有序区完成排序。
	
	// 对R[0..n-1]按递增有序进行直接插入排序
	void InsertSort(RecType R[], int n)
	{
		int i;	// 无序区指针
		int j;	// 有序区指针
		RecType tmp;

		for (i = 1; i < n; ++i)
		{
			tmp = R[i];
			j = i - 1;		// 从右向左在有序R[0..j]中找到R[i]的插入位置

			while (j >= 0 && tmp.key < R[j].key)
			{
				R[j + 1] = R[j];		// 将关键字大于R[i].key的记录后移
				j--;
			}
			R[j + 1] = tmp;		// 在j+1处插入R[i]
		}
	}

插入排序所耗费的时间是有很大差异的。最好情况是表初态为正序，此时算法的时间复杂度是O(n)；最坏情况是表初态为反序，相应的时间复杂度是O(n^2)；**算法的平均复杂度是O(n^2)**。

插入排序算法中只使用i,j和tmp这3个辅助变量，与问题规模n无关，故辅助空间复杂度为O(1)，也就是说，它使一个**就地排序**。


## 交换排序

### 冒泡排序

原理：将序列划分为无序区和有序区，通过无序区中每两个相邻记录的关键字进行比较，使关键字最小的记录到达最上端，接着，再在剩下的记录中找关键字次小的记录，并把它换在第二个位置。

	void BubbleSort(RecType R[], int n)
	{
		int i; 	// 第i趟，从0开始
		int j;  // 无序区指针
		RecType tmp;

		for (i = 0; i < n - 1; ++i)
		{
			for (j = n - 1; j > i; --j)		//找出本趟最小关键字的记录
			{
				if (R[j].key < R[j - 1].key)
				{
					tmp = R[j];		//R[j]与R[j-1]交换，将最小关键字记录前移
					R[j] = R[j - 1];
					R[j - 1] = tmp;
				}
			}
		}
	}

若表的初始状态是正序的，则一趟扫描即可完成排序，即冒泡排序最好的时间复杂度是O(n)； 若初始表是反序的，则需要进行n-1趟排序，因此，冒泡排序的最坏时间复杂度是O(n^2)； 冒泡排序的平均时间复杂度是O(n^2)。

冒泡排序算法中只使用i,j和tmp这3个辅助变量，与问题规模n无关，故辅助空间复杂度为O(1)，
也就是说，它是一个就地排序。


### 快速排序

原理：在数组中选择一个数字，接下来把数组中的数字分为两部分，比选择的数字小的数字移到数组的左边，比选择的数字大的数字移到数组的右边。实现快速排序的关键函数是Partition函数。
	
	int Partition(int data[], int length, int start, int end);
	int RandomInRange(int min, int max);
	void Swap(int *num1, int *num2);

	void QuickSort(int data[], int length, int start, int end)
	{
		if (start == end)
			return;

		int index = Partition(data, length, start, end);

		if (index > start)
			QuickSort(data, length, start, end);
		if (index < end)
			QuickSort(data, length, start, end);
	}

	int Partition(int data[], int length, int start, int end)
    {
        if(data == NULL || length <= 0 || start < 0 || end >= length)
            throw "Invalid Parameters";

        int index = RandomInRange(start, end);
        Swap(&data[index], &data[end]);

        int left = start - 1;
        int right = end;

        while (left < right)
        {
        	while (left < right && data[++left] < data[end]);
        	while (left < right && data[--right] > data[end]);

        	if (left < right)
        	{
        		Swap(&data[left], &data[right]);
        	}
        }
        Swap(&data[left], &data[end]);

        return left;

    }

    // Random
    int RandomInRange(int min, int max)
    {
        int random = rand() % (max - min + 1) + min;
        return random;
    }

    // Swap
    void Swap(int* num1, int* num2)
    {
        int temp = *num1;
        *num1 = *num2;
        *num2 = temp;
    }

快速排序的最好时间复杂度是O(nlog2(n))，最坏时间复杂度是O(n^2)，平均时间复杂度是O(nlog2(n))； 快速排序的空间复杂度O(log2(n))。

## 选择排序

### (直接)选择排序

原理：将序列分为无序区和有序区，从当前无序区中选出关键字最小的记录，和无序区的首元素交换，有序区扩大一个，循环最终完成全部排序。由于选择排序方法每一躺总是从无序区中选出全局最小(或最大)的关键字，所有适合于从大量的记录中选择一部分排序记录，例如，从10000
个记录中选择出关键字大小为前10位的记录，就适合采用选择排序。

	void SelectSort(RecType R[], int n)
	{
		int i;		// 第i趟排序(有序区指针)
		int j; 		// 无序区指针
		int k;		// 无序区最小元素指针
		RecType tmp;

		for (i = 0; i < n - 1; ++i)		// 做第i趟排序
		{
			k = i;

			// 在当前无序区R[i..n-1]中选key最小的R[k]
			for (j = i + 1; j < n; ++j)
			{
				if (R[j].key < R[k].key)
					k = j;
			}

			// 交换R[i]和R[k]
			if (k != i)			
			{
				tmp = R[i];
				R[i] = R[k];
				R[k] = tmp;
			}
		}
	}

直接选择排序的最好，最坏和平均时间复杂度都是O(n^2)。直接选择排序算法中只使用i,j,k和
tmp等4个辅助变量，与问题规模n无关，故辅助空间复杂度为O(1)，也就是说，它使一个就地排
序。

### 堆排序

堆是具有下列性质的完全二叉树：每个节点的值都大于或等于其左右孩子节点的值，称为大根堆；或者每个节点的值都小于或者等于其左右孩子节点的值，称为小根堆。

堆排序的关键是构造初始堆，采用筛选算法建堆：假若完全二叉树的某一个结点i，它的左子树、右子树已是堆，接下来需要将R[2i].key与R[2i+1].key之中的最大者与R[i].key比较，若
R[i].key较小则将其与最大孩子的关键字交换，这有可能破坏下一级的堆。于是继续采用上述方
法构造下一级的堆，直到完全二叉树中结点i构成堆为止。对于任意一棵完全二叉树，从i=[n/2]-1，反复利用上述调整方法建堆。大者“上浮”，小者被“筛选”下去。调整堆的算法如下：
	
	// 对R[low..high]进行筛选
	void sift(RecType R[], int low, int high)
	{
		int i = low;
		int j = 2 * i;	// R[j]是R[i]的左孩子
		RecType tmp = R[i];

		while (j <= high)
		{
			// 若右孩子较大，把j指向右孩子
			if (j < high && R[j].key < R[j + 1].key)
			{
				j++;
			}

			// 若R[i].key小于孩子中最大关键字
			if (tmp.key < R[j].key)
			{
				R[i] = R[j];
				i = j;
				j = 2 * i;
			}
			else 
				break;
		}
		R[i] = tmp;
	}

在初始堆构造好后，根结点一定是最大关键字结点，将堆中的根与最后一个叶子交换。由于最大元素已归位，整个待排序的元素个数减少一个，但由于根结点的改变，这n-1个结点不一定为堆，而
其左子树和右子树均为堆，调用一次sift算法将这n-1个结点调整成堆，其根结点为次大的元素，
将它放到数列的倒数第二个位置，即将堆中根与最后一个叶子交换，待排序的元素个数变为n-2个，再调整，再将根结点归位，如此这样，直到完全二叉树只剩一个根为止。算法如下：

	void HeapSort(RecType R[], int n)
	{
		int i;
		RecType tmp;

		// 循环建立初始堆
		for (i = n / 2; i >= 1; --i)
			sift(R, i, n);

		for (i = n; i >= 2; i--)
		{
			tmp = R[i];
			R[1] = R[i];
			R[i] = tmp;
			sift(R, 1, i - 1);
		}
	}

堆排序的最好，最坏和平均时间复杂度都是O(nlog2(n))，由于堆排序只使用i,j,tmp等辅助变量
故其空间复杂度为O(1)。


## 归并排序

归并排序是多次将两个或两个以上的有序表合并成一个新的有序表，最简单的归并是直接将两个有序的子表合成一个有序的表，即二路归并。

先介绍将两个有序表直接归并为一个有序表的算法Merge()。设两个有序表存放在同一数组中相邻
的位置上:R[low..mid],R[mid + 1 .. high]，先将它们合并到一个局部的暂存数组R1中，待
合并完成后将R1复制回R中。为了简便，称R[low..mid]为第一段，R[mid+1..high]为第2段。
每次从两个段中取出一个记录进行关键字的比较，将较小者放入R1中，最后将各段中余下的部分直接复制到R1中，这样R1是一个有序表，再将其复制回R中。算法如下：

	void Merge(RecType R[], int low, int mid, int high)
	{
		RecType *R1;
		int i = low; 	// i为第1段的下标
		int j = mid + 1; 	// j为第2段的下标
		int k = 0;		// k是R1的下标
		R1 = (RecType)malloc((high - low+ 1) * sizeof(RecType));

		while (i <= mid && j <= high)
		{
			// 将第1段中的记录放入R1中
			if (R[i].key <= R[j].key)
			{
				R1[k] = R[i];
				i++;
				k++;
			}
			else
			{
				R1[k] = R[j];
				j++;
				k++;
			}
		}

		// 将第1段余下的部分复制到R1
		while (i < = mid)
		{
			R1[k] = R[i];
			i++;
			k++;
		}

		// 将第2段余下的部分复制到R1
		while (j <= high)
		{
			R1[k] = R[j];
			j++;
			k++;
		}

		// 将R1复制回R中
		for (k = 0, i = low; i <= high; k++, i++)
			R[i] = R1[k];
	}

归并排序有两种实现方法：自底向上和自顶向下。设归并排序的当前区间是R[loww..high]， 采用自顶向下的方法，则递归归并的两个步骤如下：

* 分解：将当前区间R[low..high]一分为二，即求mod=(low+high)/2；递归地对两个子区间
R[low..mid]和R[mid+1..high]进行继续分解。其终结条件是子区间长度为1。

* 归并：与分解过程相反，将已排序的两个子区间R[low..mid]和R[mid+1..high]归并为一个
有序的区间R[low..high]。

对应的二路归并排序算法如下：

	void MergeSort(RecType R[], int low, int high)
	{
		int mid;
		if (low < high)
		{
			mid = (low + high) / 2;
			MergeSort(R, low, mid);
			MergeSort(R, mid + 1, high);
			Merge(R, low, mid, high);
		}
	}

归并排序的最好，最坏和平均时间复杂度都是O(nlog2(n))。归并排序过程中，每一趟需要有一个
辅助向量来暂存两个有序子表归并的结果，但在该趟排序完毕后释放其空间，所以总的辅助空间复杂度为O(n)，显然它不是就地排序。


## 总结

### 稳定的排序

| 稳定的排序 | 时间复杂度 | 空间复杂度 |
|----------|
|冒泡排序		| 最坏，平均都是O(n²)，最好是O(n) | O(1) |
|插入排序		| 最坏，平均都是O(n²)，最好是O(n) | O(1) |
|归并排序		| 最坏，平均和最好都是O(nlogn)    | O(n) |
|基数排序		| 最坏，平均和最好都是O(d(n+r))   | O(r) |

### 不稳定的排序

| 不稳定的排序 | 时间复杂度 | 空间复杂度 |
|----------|
|选择排序		| 最坏，平均和最好都是O(n²) | O(1) |
|希尔排序		| O(nlogn) or O(n^1.3) | O(1) |
|堆排序		   | 最坏，平均和最好都是O(nlogn)    | O(1) |
|快速排序		| 最好，平均都是O(nlogn)，最坏O(n²)   | O(logn) |



[1. 八大排序算法总结](http://blog.csdn.net/yexinghai/article/details/4649923 "title")
