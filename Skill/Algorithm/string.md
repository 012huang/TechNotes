
# 字符串类

1. 替换空格

2. 字符串的排列

3. 第一个只出现一次的字符

4. 翻转单词顺序VS左旋字符串

5. 把字符串转换成整数

6. 把整数转换成字符串

7. strcpy VS memcpy

8. 字符串中连续出现次数最多的子串

9. 移动字符串

10. 反转字符串

11. 两个字符串的(连续或不连续)最长的公共子串

12. 给两个字符串A和B，找出A对于B的最长前缀

### 1. 替换空格

	/* 把字符串中的每个空格替换成"%20"。每替换一个空格，长度增加2，因此替换以后
	字符串的长度等于原来的长度加上2乘以空格数目。首先，准备两个指针，P1和P2，P1指向原始字符串的末尾，而P2指向替换之后的字符串的末尾。接着向前移动指针P1，逐个把它指向的字符复制到P2指向的位置，直到碰到第一个空格为止。碰到空格后，把P1向前移动1格，在P2之前插入字符串"%20"，接着向前复制，直到碰到第二个空格，最终P1和P2指向同一位置。算法复杂度O(n)。*/

	// length为字符数组string的总容量
	void ReplaceBlank(char string[], int length)
	{
		// 第一步：判断输入参数的合法性
		if (string == NULL || length <= 0)
			return;

		// 第二步：统计原字符串的实际长度和空格个数
		// originalLength为字符串string的实际长度
		int originalLength = 0;
		int numberOfBlank = 0;
		int i = 0;
		while (string[i] != '\0')
		{
			++originalLength;
			if (string[i] == ' ')
				++numberOfBlank;
			++i;
		}

		// 第三步，初始化指针
		// newLength为把空格替换成'%20'之后的长度
		int newLength = originalLength + numberOfBlank * 2;
		if (newLength > length)
			return;

		int indexOfOriginal = originalLength;
		int indexOfNew = newLength;

		// 第四步，移动
		while (indexOfOriginal >= 0 && indexOfNew > indexOfOriginal)
		{
			if (string[indexOfOriginal] == ' ')
			{
				string[indexOfNew --] = '0';
				string[indexOfNew --] = '2';
				string[indexOfNew --] = '%';
			}
			else
			{
				string[indexOfNew --] = string[indexOfOriginal];
			}
			-- indexOfOriginal;
		}
	}

### 2. 字符串的排列
	
	/* 输入一个字符串，打印出该字符串中字符的所有排列。首先求所有可能出现在第一个
	位置的字符，即把第一个字符和后面所有的字符交换。第二步固定第一个字符，求后面所有字符的排列，典型的递归思路。*/

	void Permutation(char *pStr)
	{
		if (pStr == NULL)
			return;

		Permutation(pStr, pStr);
	}

	// pStr指向整个字符串的第一个字符,pBegin指向当前做排列操作的字符串的首字符
	void Permutation(char *pStr, char *pBegin)
	{
		if (*pBegin == '\0')
		{
			cout << pStr;
		}
		else
		{
			for (char *pCh = pBegin; *pCh != '\0'; ++pCh)
			{
				char temp = *pCh;
				*pCh = *pBegin;
				*pBegin = temp;

				Permutation(pStr, pBegin + 1);

				temp = *pCh;
				*pCh = *pBegin;
				*pBegin = temp;
			}
		}
	}

### 3. 第一个只出现一次的字符

	/* 在字符串中找出第一个只出现一次的字符。最直观的想法是从头开始扫描这个字符串中
	的每个字符。当访问到某字符时拿这个字符和后面的每个字符相比较，如果在后面没有发现重复的字符，则该字符就是只出现一次的字符。这种思路的算法复杂度为O(n^2)。考虑
	O(n)的算法，字符是一个长度为8的数据类型，因此总共有256种可能。于是我们创建一个
	长度为256的数组，每个字母根据其ASCII码作为数组的下标对应数组的一个数字，而数组中存储的是每个字符出现的次数。这样我们就创建了一个大小为256，以字符ASCII码为键值的哈希表。

	char FirstNotRepeatingChar(char *pString)
	{
		if (pString == NULL)
			return '\0';

		// 数据初始化
		const int tableSize = 256;
		unsigned int hashTable[tableSize];
		for (unsigned int i = 0; i < tableSize; ++i)
			hashTable[i] = 0;

		// 统计次数
		char *pHashKey = pString;
		while (*pHashKey != '\0')
			hashTable[*(pHashKey++)]++;

		// 找出第一个只出现一次的字符
		pHashKey = pString;
		while (*pHashKey != '\0')
		{
			if (hashTable[*pHashKey] == 1)
				return *pHashKey;

			pHashKey++;
		}

		return '\0';
	}

### 4. 翻转单词顺序VS左旋字符串

	(1)输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变，为简单起见，
	标点符号和普通字母一样处理。例如输入字符串"I am a student."，则输出"student. a am I"。
	/* 第一步翻转句子中所有的字符；第二步再翻转每个单词中字符的顺序。*/

	// 函数Reverse翻转字符串中的一段
	void Reverse(char *pBegin, char *pEnd)
	{
		if (pBegin == NULL || pEnd == NULL)
			return;

		while (pBegin < pEnd)
		{
			char temp = *pBegin;
			*pBegin = *pEnd;
			*pEnd = temp;

			pBegin++;
			pEnd--;
		}
	}

	// 接着用Reverse函数先翻转整个句子，再翻转句子中的每个单词
	char* ReverseSentence(char *pData)
	{
		if (pData == NULL)
			return NULL;

		// pBegin指向第一个字符
		char *pBegin = pData;

		// pEnd指向最后一个字符
		char *pEnd = pData;
		while (*pEnd != '\0')
			pEnd++;
		pEnd--;

		// 翻转整个句子
		Reverse(pBegin, pEnd);

		// 翻转句子中的单词
		pBegin = pEnd = pData;
		while (*pBegin != '\0')
		{
			if (*pBegin == ' ')
			{
				pBegin++;
				pEnd++;
			}
			else if (*pEnd == ' ' || *pEnd == '\0')
			{
				pEnd--;
				Reverse(pBegin, pEnd);
				pBegin = ++pEnd;
			}
			else
			{
				pEnd++;
			}
		}

		return pData;
	}

	(2) 字符串左旋指把字符串前面的若干个字符转移到字符串的尾部。比如输入字符串
	"abdef"，左旋两位，得到"defab"。

	/* 思路：调用三次Reverse函数实现 */
	char* LeftRotateString(char* pStr, int n)
    {
        if(pStr != NULL)
        {
            int nLength = static_cast<int>(strlen(pStr));
            if(nLength > 0 && n > 0 && n < nLength)
            {
                char* pFirstStart = pStr;
                char* pFirstEnd = pStr + n - 1;
                char* pSecondStart = pStr + n;
                char* pSecondEnd = pStr + nLength - 1;

                // 翻转字符串的前面n个字符
                Reverse(pFirstStart, pFirstEnd);
                // 翻转字符串的后面部分
                Reverse(pSecondStart, pSecondEnd);
                // 翻转整个字符串
                Reverse(pFirstStart, pSecondEnd);
            }
        }

        return pStr;
    }

### 5. 把字符串转换成整数
	
	/* 注意考虑空指针，空字符串，正负号，溢出，另外还需判断整数是否发生上溢出或者
	下溢出，正整数的最大值是0x7FFF FFFF，最小的负整数是0x8000 0000。*/

	long long StrToIntCore(const char *digit, bool minus);

	// 定义全局变量g_Status来标记是不是遇到了非法输入
	enum Status {kValid = 0, kInvalid};
	int g_nStatus = kValid;

	int StrToInt(const char *str)
	{
		g_nStatus = kInvalid;
		long long num = 0;

		if (str != NULL && *str != '\0') // 不是空指针也不是空字符串
		{
			bool minus = false;
			if (*str == '+')
				str++;
			else if (*str == '-')
			{
				str++;
				minus = true;
			}

			if (*str != '\0')	// 继续检查第二个字符不是空字符串
			{
				num = StrToIntCore(str, minus);
			}
		}

		return (int)num;
	}

	long long StrToIntCore(const char *digit, bool minus)
	{
		long long num = 0;

		while (*digit != '\0')
		{
			if (*digit >= '0' && *digit <= '9')
			{
				int flag = minus ? -1 : 1;
				num = num * 10 + flag * (*digit - '0');

				if ((!minus && num > 0x7FFFFFFF)
					|| (minus && num < (signed int)0x80000000))
				{
					num = 0;
					break;
				}

				digit++;
			}
			else
			{
				num = 0;
				break;
			}
		}

		if (*digit == '\0')
		{
			g_nStatus = kValid;
		}

		return num;
	}

### 6. 把整数转换成字符串
	
	/* 整数转化成字符串，可以采用加'0'，再逆序的方法，整数加'0'会隐性地转化成char类型 */

	#define abs(cond) ((cond) > 0 ? (cond) : (-cond))
	char *IntToStr(const int value)
	{
		char *str = NULL;
		char strtmp[32] = {'\0'};
		int absval = abs(value);
		int i = 0;
		int j;

		while (absval != 0)
		{
			strtmp[i] = (absval % 10) + '0';
			++i;
			absval = absval / 10;
		}
		
		if (value < 0)
			strtmp[i] = '-';

		while (i >= 0)
		{
			*str = strtmp[i];
			++str;
			--i;
		}
		*str = '\0';

		return str;
	}

### 7. strcpy VS memcpy

	/* strcpy和memcpy的区别：strcpy只用于字符串的复制，memcpy则可用于一般内存的
	复制，比如字符数组，整型和结构体等。返回strDest的原始值使函数能够支持链式表达
	式，如int length = strlen(strcpy(strA, strB));

	char* strcpy(char *strDest, const char *strSrc)
	{
		// 检查指针的有效性
		if ((strDest == NULL) || (strSrc == NULL))
			throw "Invalid argument(s)";

		// 保留strDest的头指针
		char *strDestCopy = strDest;

		// 先赋值，再判断是否为零，这样会给strDest赋上结尾零
		while ((*strDest++ = *strSrc++) != '\0');

		return strDestCopy;
	}

### 8. 字符串中连续出现次数最多的子串
基本算法描述: 
    给出一个字符串abababa
    1.穷举出所有的后缀子串 
        substrs[0] = abababa; 
        substrs[1] = bababa; 
        substrs[2] = ababa;
        substrs[3] = baba;
        substrs[4] = aba;
        substrs[5] = ba; 
        substrs[6] = a; 
    2.然后进行比较 
        substrs[0]比substrs[1]多了一个字母,如果说存在连续匹配的字符,那么 
        substrs[0]的第1个字母要跟substrs[1]首字母匹配,同理 
        substrs[0]的前2个字母要跟substrs[2]的前2个字母匹配(否则不能叫连续匹配) 
        substrs[0]的前n个字母要跟substrs[n]的前n个字母匹配. 
        如果匹配的并记下匹配次数.如此可以求得最长连续匹配子串. 

    // 这里只输出其中一个，如果要全都输出，可放入到map中。
    pair<int, string> fun(const string &str)  
    {  
        vector<string> substrs;  
        int maxcount = 1, count = 1;  
        string substr;  
        int i, len = str.length();  

        // 把str字符串中的子串按每次把头部减少一个的方式插入到vector向量中
        for(i = 0; i < len; ++i)  
           substrs.push_back(str.substr(i, len-i));   

        // 后缀数组的第一个元素，开始遍历
        for(i = 0; i < len; ++i)  
        {  
        	// 后缀数组中substrs[i]之后的元素依次与substrs[i]比较
            for(int j = i+1; j < len; ++j)  
            {  
                count = 1;  
                // 如果前j-i个元素相同,如果有连续一个子串出现就继续遍历vector的下一个子串中的
                // 和现在出现相同子串的地方的下一个或几个字符
                if(substrs[i].substr(0, j-i) == substrs[j].substr(0,j-i))  
                {  
                    ++count;  

                    // 子串中前j-i个元素相同
                    for(int k=j+(j-i); k<len; k+=j-i)  
                    {  
                        if (substrs[i].substr(0,j-i) == substrs[k].substr(0, j-i))  
                            ++count;  
                        else  
                            break;  
                    }  
                    if(count > maxcount)  
                    {  
                        maxcount = count;  
                        substr=substrs[i].substr(0, j-i);  
                    }  
                }  
            }  
        }  
        return make_pair(maxcount, substr);  
    }

### 9. 移动字符串

	/* 传入参数char *str和m，将str中字符串的倒数m个字符移到字符串前面，其余依次向右移。如abcdefghi,m=3,那么移动之后就是ghiabcdef。使用最后一个'\0'来临时存储，字符串整体向右移动一个字节。*/

	void fun(char *str, int m)
	{
  		int i = 0;
  		int len = strlen(w);
     	if (m > len) 
     		m = len;
  		while (m > 0)
  		{
    		for(i = len, m--; i > 0; i--, w[i] = w[len]) 
    		w[i] = w[i-1];
  		}
  		w[len-m] = '\0';
	}

### 10. 反转字符串

	/* 要求优化速度，优化空间 */
	
	char* strreverse(const char *strSrc)
	{
		// 检查指针的有效性
		if (strSrc == NULL)
			throw "Invalid argument(s)";

		// 新建字符串指针
		char *strDest = new char[strlen(str) + 1];
		strcpy(strDest, strSrc);
		
		// 指向strDest的头指针
		char *pLeft = strDest;
		
		// 指向strDest的尾指针
		char *pRight = strDest + strlen(str) - 1;
		
		while (pRight > pLeft)
		{
			*pRight ^= *pLeft;
			*pLeft ^= *pRight;
			*pRight ^= *pLeft;
			
			--pRight;
			++pLeft;
		}
		
		return strDest;
	}





### 11. 两个字符串的(连续或不连续)最长的公共子串

### 12. 给两个字符串A和B，找出A对于B的最长前缀。
例：A: abcdeabcdesa B: description 输出des。



