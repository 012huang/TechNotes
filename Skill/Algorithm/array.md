
# 数组类

1.  二维数组中的查找

2.  旋转数组的最小数字

3.  调整数组顺序使奇数位于偶数前面

4.  顺时针打印矩阵

5.  数组中出现次数超过一半的数字

6.  数组中最小的k个数

7.  连续子数组的最大和

8.  把数组排成最小的数

9.  数组中的逆序对

10. 数字在排序数组中出现的次数

11. 数组中只出现一次的数字

12. 和为s的两个数字VS和为s的连续正数序列

### 1. 二维数组中的查找

	/* 首先选取数组中右上角的数字。如果该数字等于要查找的数字，查找过程结束；如果该数字
	大于要查找的数字，剔除这个数字所在的列；如果该数字小于要查找的数字，剔除这个数字所在
	的行。
	*/

	// 二维数组matrix中，每一行都从左到右递增排序，
	// 每一列都从上到下递增排序
	bool Find(int *matrix, int rows, int columns, int number)
	{
		bool found = false;

		if (matrix != NULL && rows > 0 && columns > 0)
		{
			int row = 0;
			int column = columns - 1;
			while (row < rows && column >= 0)
			{
				if (matrix[row * columns + column] == number)
				{
					found = true;
					break;
				}
				else if (matrix[row * columns + column] > number)
					--column;
				else
					++row;
			}
		}

		return found;
	}

### 2. 旋转数组的最小数字
	
	/* 基于二分查找的思路，用两个指针分别指向数组的第一个元素和最后一个元素，找数组中间
	的元素，如果该中间元素大于或者等于第一个指针指向的元素，它位于前面的递增子数组，将第一个指针指向该中间元素，如果该中间元素小于或者等于第二个指针指向的元素，它位于后面的递增子数组，将第二个指针指向该中间元素。最终，第一个指针指向前面子数组的最后一个元素，而第二个指针指向后面子数组的第一个元素。也就是它们最终会指向两个相邻的元素，而第二个指针指向的刚好是最小的元素。
	注意：把排序数组的前面的0个元素搬到最后面以及首，尾和中间三个元素相等这两种情况。
	*/

	int Min(int *numbers, int length)
	{
		if (numbers == NULL || length <= 0)
			throw new std::exception("Invalid parameters");

		int index1 = 0;
		int index2 = length - 1;
		int indexMid = index1;
		while (numbers[index1] >= numbers[index2])
		{
			if (index2 - index1 == 1)
			{
				indexMid = index2;
				break;
			}

			indexMid = (index1 + index2) / 2;

			// 如果下标为index1、index2和indexMid指向的三个数字相等，则顺序查找
			if (numbers[index1] == numbers[index2] 
				&& numbers[indexMid] == numbers[index1])
				return MinInOrder(numbers, index1, index2);

			if (numbers[indexMid] >= numbers[index1])
				index1 = indexMid;
			else if (numbers[indexMid] <= numbers[index2])
				index2 = indexMid;
		}

		return numbers[indexMid];
	}

	int MinInOrder(int *numbers, int index1, int index2)
	{
		int result = numbers[index1];
		for (int i = index1 + 1; i <= index2; ++i)
		{
			if (result > numbers[i])
				result = numbers[i];
		}

		return result;
	}

### 3. 调整数组顺序使奇数位于偶数前面

	/* 使用两个指针，第一个指针初始化时指向数组的第一个数字，它只向后移动；第二个指针初
	始化时指向数组的最后一个数字，它只向前移动。在两个指针相遇之前，第一个指针总是位于第二个指针的前面。如果第一个指针指向的数字是偶数，并且第二个指针指向的数字是奇数，我们就交换这两个数字。
	*/
	
	void ReorderOddEven(int *pData, unsigned int length)
	{
		if (pData == NULL || length == 0)
			return;

		int *pBegin = pData;
		int *pEnd   = pData + length - 1;

		while (pBegin < pEnd)
		{
			// 向后移动pBegin,直到它指向偶数
			while (pBegin < pEnd && (*pBegin & 0x1) != 0)
				pBegin++;

			// 向前移动pEnd,直到它指向奇数
			while (pBegin < pEnd && (*pEnd & 0x1) == 0)
				pEnd--;

			if (pBegin < pEnd)
			{
				int temp = *pBegin;
				*pBegin = *pEnd;
				*pEnd = temp;
			}
		}
	}

### 4. 顺时针打印矩阵
	
	/* 把矩阵看成由若干个顺时针方向的圈组成，从第0圈，即最外一圈开始打印，第0圈左上角的
	坐标是(0, 0)，第1圈左上角的坐标是(1, 1)，第start圈的左上角坐标是(start, start).
	第start圈的行数为rows - start * 2,列数为columns - start * 2,若这两个数都大于0,
	则循环继续，第start圈的endX = columns - 1 - start, endY = rows - 1 - strart.

	(start, start) ----> (start, endX)
		   |					|
		   |					|
		   V                    V
	(endY, start) -----> (endY, endX)

	endX - start + 1 = columns - start * 2;
	endY - start + 1 = rows - start * 2;
	*/

	void PrintMatrixClockwisely(int** numbers, int columns, int rows)
    {
        if(numbers == NULL || columns <= 0 || rows <= 0)
            return;

        int start = 0;

        while(columns > start * 2 && rows > start * 2)
        {
            PrintMatrixInCircle(numbers, columns, rows, start);

            ++start;
        }
    }

    void PrintMatrixInCircle(int** numbers, int columns, int rows, int start)
    {
        int endX = columns - 1 - start;
        int endY = rows - 1 - start;

        // 从左到右打印一行
        for(int i = start; i <= endX; ++i)
        {
            int number = numbers[start][i];
            printNumber(number);
        }

        // 从上到下打印一列
        if(start < endY)
        {
            for(int i = start + 1; i <= endY; ++i)
            {
                int number = numbers[i][endX];
                printNumber(number);
            }
        }

        // 从右到左打印一行
        if(start < endX && start < endY)
        {
            for(int i = endX - 1; i >= start; --i)
            {
                int number = numbers[endY][i];
                printNumber(number);
            }
        }

        // 从下到上打印一行
        if(start < endX && start < endY - 1)
        {
            for(int i = endY - 1; i >= start + 1; --i)
            {
                int number = numbers[i][start];
                printNumber(number);
            }
        }
    }

### 5. 数组中出现次数超过一半的数字
	
	/* 如果把这个数组排序，那么排序之后位于数组中间的数字一定就是那个出现次数超过数组长
	度一半的数字。也就是说，这个数字就是统计学上的中位数，即长度为n的数组中第n/2大的数
	字，利用随机快速排序中的Partition函数来实现。
	注意：该方法会修改输入的数组。*/

	bool g_bInputInvalid = false;
	bool CheckInvalidArray(int* numbers, int length);
	bool CheckMoreThanHalf(int* numbers, int length, int number);
	int Partition(int data[], int length, int start, int end);

	int MoreThanHalfNum_Solution1(int *numbers, int length)
	{
		if (CheckInvalidArray(numbers, length))
			return 0;

		int middle = length >> 1;
		int start = 0;
		int end = length - 1;
		int index = Partition(numbers, length, start, end);
		while (inex != middle)
		{
			if (index > middle)
			{
				end = index - 1;
				index = Partition(numbers, length, start, end);
			}
			else
			{
				start = index + 1;
				index = Partition(numbers, length, start, end);
			}
		}

		int result = numbers[middle];
		if (!CheckMoreThanHalf(numbers, length, result))
			result = 0;

		return result;
	}

	/* 数组中有一个数字出现的次数超过数组长度的一半，也就是说它出现的次数比其他所有数字
	出现的和还要多。因此我们可以在遍历数组的时候保存两个值：一个是数组中的一个数字，一个
	是次数。当我们遍历到下一个数字的时候，如果下一个数字和我们之前保存的数字相同，则次数
	加1；如果下一个数字和我们之前保存的数字不同，则次数减1。如果次数为零，我们需要保存下
	一个数字，并把次数设为1。由于我们要找的数字出现的次数比其他所有数字出现的次数之和还
	要多，那么要找的数字肯定是最后一次把次数设为1时对应的数字。 
	注意：该方法不会修改输入数据。 */

	int MoreThanHalfNum_Solution2(int* numbers, int length)
    {
        if(CheckInvalidArray(numbers, length))
            return 0;
     
        int result = numbers[0];
        int times = 1;
        for(int i = 1; i < length; ++i)
        {
            if(times == 0)
            {
                result = numbers[i];
                times = 1;
            }
            else if(numbers[i] == result)
                times++;
            else
                times--;
        }
     
        if(!CheckMoreThanHalf(numbers, length, result))
            result = 0;
     
        return result;
    }

    // 判断输入数据是否合法
    bool CheckInvalidArray(int* numbers, int length)
    {
        g_bInputInvalid = false;
        if(numbers == NULL && length <= 0)
            g_bInputInvalid = true;

        return g_bInputInvalid;
    }

    // 判断数组中出现频率最高的数字有没有超过一半
    bool CheckMoreThanHalf(int* numbers, int length, int number)
    {
        int times = 0;
        for(int i = 0; i < length; ++i)
        {
            if(numbers[i] == number)
                times++;
        }
     
        bool isMoreThanHalf = true;
        if(times * 2 <= length)
        {
            g_bInputInvalid = true;
            isMoreThanHalf = false;
        }

        return isMoreThanHalf;
    }

### 6. 数组中最小的k个数
	
	/* 如果基于数组的第K个数字来调整，使得比第K个数字小的所有数字都位于数组的左边，比第
	K个数字大的所有数字都位于数组的右边，这样调整之后，位于数组左边的K个数字就是最小的K
	个个数字(不一定有序)，基于Partition函数实现。
	注意：该方法会修改输入的数组，复杂度O(n)。 */

	void GetLeastNumbers_Solution1(int *input, int n, int *output, int k)
	{
		if (input == NULL || output == NULL || k > n || n <= 0 || k <= 0)
			return;

		int start = 0;
		int end = n - 1;
		int index = Partition(input, n, start, end);
		while (index != k - 1)
		{
			if (index > k - 1)
			{
				end = index - 1;
				index = Partition(input, n, start, end);
			}
			else
			{
				start = index + 1;
				index = Partition(input, n, start, end);
			}
		}

		for (int i = 0; i < k; ++i)
			output[i] = input[i];
	}
	
	/* 如果是从海量数据中找出最小的k个数字，则可以用最大堆来实现，利用STL中的set和
	multiset来实现，复杂度O(nlogk)。思想：创建一个大小为K的数据容器来存储最小的k个
	数字，从输入的n个整数中读入一个数，如果容器中已有的数字少于k个，则直接把读入的数字
	装进容器中，否则找出已有的k个数中的最大值，将它跟待插入的整数进行比较，如果它比待插
	入的整数大，则将待插入的树代替该最大值，否则读取下一个。 */

	typedef multiset<int, greater<int> >            intSet;
    typedef multiset<int, greater<int> >::iterator  setIterator;

    void GetLeastNumbers_Solution2(const vector<int>& data, intSet& leastNumbers, int k)
    {
        leastNumbers.clear();

        if(k < 1 || data.size() < k)
            return;

        vector<int>::const_iterator iter = data.begin();
        for(; iter != data.end(); ++ iter)
        {
            if((leastNumbers.size()) < k)
                leastNumbers.insert(*iter);

            else
            {
                setIterator iterGreatest = leastNumbers.begin();

                if(*iter < *(leastNumbers.begin()))
                {
                    leastNumbers.erase(iterGreatest);
                    leastNumbers.insert(*iter);
                }
            }
        }
    }

### 7. 连续子数组的最大和
	
	/* 当以第i-1个数字结尾的子数组中所有数字的和小于0时，则以第i个数字结尾的子数组就是
	第i个数字本身，如果以第i-1个数字结尾的子数组中所有数字的和大于0，与第i个数字累加就
	得到以第i个数字结尾的子数组中所有数字的和。 */

	bool g_InvalidInput = false;

	int FindGreatSumOfSubArray(int *pData, int nLength)
	{
		if ((pData == NULL) || (nLength <= 0))
		{
			g_InvalidInput = true;
			return 0;
		}

		g_InvalidInput = false;

		int nCurSum = 0;
		int nGreatestSum = 0x80000000;
		for (int i = 0; i < nLength; ++i)
		{
			if (nCurSum <= 0)
				nCurSum = pData[i];
			else
				nCurSum += pData[i];

			if (nCurSum > nGreatestSum)
				nGreatestSum = nCurSum;
		}

		return nGreatestSum;
	}

### 8. 把数组排成最小的数
	
	/* 给出数字m和n，怎么得到数字mn和nm并比较它们的大小？考虑到一个潜在的问题就是m和n
	都在int能表达的范围内，把mn和nm用int表示就有可能溢出，所以这是一个大数问题。一个
	非常直观的解决大数问题的方法就是把数字转换成字符串。由于把数字mn和nm的位数是相同的，
	因此只需要按照字符串大小的比较规则就可以了。 */

	// int型整数用十进制表示最多只有10位
    const int g_MaxNumberLength = 10;
     
    char* g_StrCombine1 = new char[g_MaxNumberLength * 2 + 1];
    char* g_StrCombine2 = new char[g_MaxNumberLength * 2 + 1];
     
    void PrintMinNumber(int* numbers, int length)
    {
        if(numbers == NULL || length <= 0)
            return;
     
        char** strNumbers = (char**)(new int[length]);
        for(int i = 0; i < length; ++i)
        {
            strNumbers[i] = new char[g_MaxNumberLength + 1];
            sprintf(strNumbers[i], "%d", numbers[i]);
        }
     
        qsort(strNumbers, length, sizeof(char*), compare);
     
        for(int i = 0; i < length; ++i)
            printf("%s", strNumbers[i]);
        printf("\n");
     
        for(int i = 0; i < length; ++i)
            delete[] strNumbers[i];
        delete[] strNumbers;
    }
     
    // 如果[strNumber1][strNumber2] > [strNumber2][strNumber1], 返回值大于0
    // 如果[strNumber1][strNumber2] = [strNumber2][strNumber1], 返回值等于0
    // 如果[strNumber1][strNumber2] < [strNumber2][strNumber1], 返回值小于0
    int compare(const void* strNumber1, const void* strNumber2)
    {
        // [strNumber1][strNumber2]
        strcpy(g_StrCombine1, *(const char**)strNumber1);
        strcat(g_StrCombine1, *(const char**)strNumber2);
     
        // [strNumber2][strNumber1]
        strcpy(g_StrCombine2, *(const char**)strNumber2);
        strcat(g_StrCombine2, *(const char**)strNumber1);
     
        return strcmp(g_StrCombine1, g_StrCombine2);
    }

### 9. 数组中的逆序对
	
	/* 先把数组分隔成子数组，先统计出子数组内部的逆序对的数目，然后再统计出两个相邻子数
	组之间的逆序对的数目，在统计逆序对的过程中，还需要对数组进行排序，这个过程实际上就是
	归并排序。*/

	int InversePairsCore(int* data, int* copy, int start, int end);

    int InversePairs(int* data, int length)
    {
        if(data == NULL || length < 0)
            return 0;

        int* copy = new int[length];
        for(int i = 0; i < length; ++ i)
            copy[i] = data[i];

        int count = InversePairsCore(data, copy, 0, length - 1);
        delete[] copy;

        return count;
    }

    int InversePairsCore(int* data, int* copy, int start, int end)
    {
        if(start == end)
        {
            copy[start] = data[start];
            return 0;
        }

        int length = (end - start) / 2;

        int left = InversePairsCore(copy, data, start, start + length);
        int right = InversePairsCore(copy, data, start + length + 1, end);

        // i初始化为前半段最后一个数字的下标
        int i = start + length; 
        // j初始化为后半段最后一个数字的下标
        int j = end; 
        int indexCopy = end;
        int count = 0;
        while(i >= start && j >= start + length + 1)
        {
            if(data[i] > data[j])
            {
                copy[indexCopy--] = data[i--];
                count += j - start - length;
            }
            else
            {
                copy[indexCopy--] = data[j--];
            }
        }

        for(; i >= start; --i)
            copy[indexCopy--] = data[i];

        for(; j >= start + length + 1; --j)
            copy[indexCopy--] = data[j];

        return left + right + count;
    }

### 10. 数字在排序数组中出现的次数

	/* 输入的数组是排序的，很自然地想到用二分查找算法。用二分查找找到第一个和最后一个K。
	如果中间的数字和k相等，先判断这个数字是不是第一个k，如果位于中间数字的前面一个不是
	K，此时中间的数字刚好就是第一个K。找最后一个K也类似。复杂度O(log n)。*/

	int GetFirstK(int* data, int length, int k, int start, int end);
    int GetLastK(int* data, int length, int k, int start, int end);

    int GetNumberOfK(int* data, int length, int k)
    {
        int number = 0;

        if(data != NULL && length > 0)
        {
            int first = GetFirstK(data, length, k, 0, length - 1);
            int last = GetLastK(data, length, k, 0, length - 1);
            
            if(first > -1 && last > -1)
                number = last - first + 1;
        }

        return number;
    }

    // 找到数组中第一个k的下标。如果数组中不存在k，返回-1
    int GetFirstK(int* data, int length, int k, int start, int end)
    {
        if(start > end)
            return -1;

        int middleIndex = (start + end) / 2;
        int middleData = data[middleIndex];

        if(middleData == k)
        {
            if((middleIndex > 0 && data[middleIndex - 1] != k) 
                || middleIndex == 0)
                return middleIndex;
            else
                end  = middleIndex - 1;
        }
        else if(middleData > k)
            end = middleIndex - 1;
        else
            start = middleIndex + 1;

        return GetFirstK(data, length, k, start, end);
    }

    // 找到数组中最后一个k的下标。如果数组中不存在k，返回-1
    int GetLastK(int* data, int length, int k, int start, int end)
    {
        if(start > end)
            return -1;

        int middleIndex = (start + end) / 2;
        int middleData = data[middleIndex];

        if(middleData == k)
        {
            if((middleIndex < length - 1 && data[middleIndex + 1] != k) 
                || middleIndex == length - 1)
                return middleIndex;
            else
                start  = middleIndex + 1;
        }
        else if(middleData < k)
            start = middleIndex + 1;
        else
            end = middleIndex - 1;

        return GetLastK(data, length, k, start, end);
    }

### 11. 数组中只出现一次的数字
	
	/* 任何一个数字异或它自己都等于0。从头到尾依次异或数组中的每一个数字，那么最终得到的
	结果就是两个只出现一次的数字的异或结果。由于这两个数字肯定不一样，那么异或的结果肯定
	不为0，也就是说在这个结果数字的二进制表示中至少就有一位为1.假设第k位为结果数字的二进
	制表示中第一个为1的位置，根据第k位是不是1把原数组分成两个子数组，第一个子数组中每个数字的第k位都是1，而第二个子数组中每个数字的第k位都是0。*/

	unsigned int FindFirstBitIs1(int num);
	bool IsBit1(int num, unsigned int indexBit);

	void FindNumsAppearOnce(int data[], int length, int *num1, int *num2)
	{
		if (data == NULL || length < 2)
			return;

		int resultExclusiveOR = 0;
		for (int i = 0; i < length; ++i)
			resultExclusiveOR ^= data[i];

		unsigned int indexOf1 = FindFirstBitIs1(resultExclusiveOR);

		*num1 = *num2 = 0;
		for (int j = 0; j < length; ++j)
		{
			if (IsBit1(data[j], indexOf1))
				*num1 ^= data[j];
			else
				*num2 ^= data[j];
		}
	}

	// 找到num从右边数起第一个是1的位
	unsigned int FindFirstBitIs1(int num)
	{
		int indexBit = 0;
		while (((num & 1) == 0) && (indexBit < 8 * sizeof(int)))
		{
			num = num >> 1;
			++indexBit;
		}

		return indexBit;
	}

	// 判断数字num的第indexBit是不是1
	bool IsBit1(int num, unsigned int indexBit)
	{
		num = num >> indexBit;
		return (num & 1);
	}

### 12. 和为s的两个数字VS和为s的连续正数序列

	(1) 输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果
	有多对数字的和等于s，输出任意一对即可。
	
	/* 定义两个指针，第一个指针指向数组的第一个数字，第二个指针指向数组的最后一个，如果
	两个指针指向的数字和大于s，则第二个指针向前移动一个数字，否则第一个指针向后移动一个数字。*/

	bool FindNumbersWithSum(int data[], int length, int sum,
							int *num1, int *num2)
	{
		bool found = false;
		if (length < 1 || num1 == NULL || num2 == NULL)
			return found;

		int right = length - 1;
		int left = 0;

		while (right > left)
		{
			long long curSum = data[right] + data[left];

			if (curSum == sum)
			{
				*num1 = data[left];
				*num2 = data[right];
				found = true;
				break;
			}
			else if (curSum > sum)
				right--;
			else
				left++;
		}

		return found;
	}

	(2) 输入一个正数，打印出所有和为s的连续正数序列(至少含有两个数)

	/* 考虑用两个数small和big分别表示序列的最小值和最大值。首先把small初始化为1，big初
	始化为2。如果从small到big的序列的和大于s，我们可以从序列中去掉较小的值，也就是增大
	smll的值。如果从small到big的序列的和于s，增大big的值。这个序列至少要有两个数字，我们一直增加small到(1+s)/2为止。*/

	void PrintContinuousSequence(int small, int big);

    void FindContinuousSequence(int sum)
    {
        if(sum < 3)
            return;

        int small = 1; 
        int big = 2;
        int middle = (1 + sum) / 2;
        int curSum = small + big;

        while(small < middle)
        {
            if(curSum == sum)
                PrintContinuousSequence(small, big);

            while(curSum > sum && small < middle)
            {
                curSum -= small;
                small ++;

                if(curSum == sum)
                    PrintContinuousSequence(small, big);
            }

            big ++;
            curSum += big;
        }
    }

    void PrintContinuousSequence(int small, int big)
    {
        for(int i = small; i <= big; ++ i)
            printf("%d ", i);

        printf("\n");
    }
