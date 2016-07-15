# 链表类

1. 求单链表结点的个数

2. 反转链表

3. 从尾到头打印链表

4. 在O(1)时间删除链表结点

5. 查找链表中倒数第K个结点

6. 查找链表的中间结点

7. 判断单链表是否有环

8. 合并两个排序的链表

9. 复杂链表的复制

10. 判断两个单链表是否相交

11. 求两个链表的第一个公共结点

12. 已知单链表存在环，求进入环中的第一个结点

### 1. 求单链表结点的个数

	// 求单链表中结点的个数
	unsigned int GetListLength(ListNode * pHead)
	{
		if(pHead == NULL)
			return 0;

		unsigned int nLength = 0;
		ListNode * pCurrent = pHead;
		while(pCurrent != NULL)
		{
			nLength++;
			pCurrent = pCurrent->m_pNext;
		}
		return nLength;
	}

### 2. 反转链表

	ListNode* ReverseList(ListNode* pHead)
	{
    	ListNode* pReversedHead = NULL;
    	ListNode* pCurrent = pHead;			// 当前结点
    	ListNode* pPrev = NULL;				// 前一个结点
    	while(pNode != NULL)
    	{
        	ListNode* pNext = pCurrent->m_pNext;	// 下一个结点

        	if(pNext == NULL)
            	pReversedHead = pNode;

        	pCurrent->m_pNext = pPrev;

        	pPrev = pCurrent;
        	pCurrent = pNext;
    	}

    	return pReversedHead;
	}

### 3. 从尾到头打印链表
	
	/* 每经过一个结点的时候，把该结点放到一个栈中，当遍历完整个链表后，再从栈顶开始逐个
	输出结点的值，此时输出的结点的顺序已经反转过来了
	*/

	void PrintListReversingly_Iteratively(ListNode* pHead)
	{
    	std::stack<ListNode*> nodes;

    	ListNode* pNode = pHead;
    	while(pNode != NULL)
    	{
    	    nodes.push(pNode);
    	    pNode = pNode->m_pNext;
    	}

    	while(!nodes.empty())
    	{
    	    pNode = nodes.top();
    	    printf("%d\t", pNode->m_nValue);
    	    nodes.pop();
    	}
	}

	/* 用递归实现，先递归输出它后面的结点，再输出该结点自身 */
	void PrintListReversingly_Recursively(ListNode* pHead)
	{
    	if(pHead != NULL)
    	{
        	if (pHead->m_pNext != NULL)
        	{
        	    PrintListReversingly_Recursively(pHead->m_pNext);
        	}
 
        	printf("%d\t", pHead->m_nValue);
    	}
	}

### 4. 在O(1)时间删除链表结点

	/* 要删除结点i，先把i的下一个结点j的内容复制到i，然后把i的指针指向结点j的下一个结点。
	此时再删除结点j，其效果刚好是把结点i给删除了。注意尾结点，头结点的情况。另外，该代码
	基于一个假设，要删除的结点在链表中。
	*/

	void DeleteNode(ListNode** pListHead, ListNode* pToBeDeleted)
	{
    	if(!pListHead || !pToBeDeleted)
        	return;

    	// 要删除的结点不是尾结点
    	if(pToBeDeleted->m_pNext != NULL)
    	{
    	    ListNode* pNext = pToBeDeleted->m_pNext;
    	    pToBeDeleted->m_nValue = pNext->m_nValue;
    	    pToBeDeleted->m_pNext = pNext->m_pNext;
 	
    	    delete pNext;
    	    pNext = NULL;
    	}
    	// 链表只有一个结点，删除头结点（也是尾结点）
    	else if(*pListHead == pToBeDeleted)
    	{
    	    delete pToBeDeleted;
    	    pToBeDeleted = NULL;
    	    *pListHead = NULL;
    	}
    	// 链表中有多个结点，删除尾结点
    	else
    	{
    	    ListNode* pNode = *pListHead;
    	    while(pNode->m_pNext != pToBeDeleted)
    	    {
    	        pNode = pNode->m_pNext;            
    	    }
 
    	    pNode->m_pNext = NULL;
    	    delete pToBeDeleted;
    	    pToBeDeleted = NULL;
    	}
	}

### 5. 查找链表中倒数第K个结点
	
	/* 第一个指针从链表的头指针开始遍历向前走k-1，第二个指针保持不动；从第k步开始，第二个
	指针也开始从链表的头指针开始遍历。由于两个指针的距离保持在k-1，当第一个(走在前面的)指
	针到达链表的尾结点时，第二个指针(走在后面的)指针正好是倒数第k个结点。
	*/ 

	ListNode* FindKthToTail(ListNode* pListHead, unsigned int k)
	{
    	if(pListHead == NULL || k == 0)
    	    return NULL;

    	ListNode *pAhead = pListHead;
    	ListNode *pBehind = NULL;

    	for(unsigned int i = 0; i < k - 1; ++ i)
    	{
    	    if(pAhead->m_pNext != NULL)
    	        pAhead = pAhead->m_pNext; 		// 链表结点个数小于k
    	    else
    	    {
    	        return NULL;
    	    }
    	}

    	pBehind = pListHead;
    	while(pAhead->m_pNext != NULL)
    	{
    	    pAhead = pAhead->m_pNext;
    	    pBehind = pBehind->m_pNext;
    	}

    	return pBehind;
	}

### 6. 查找链表的中间结点

	/* 此题可应用于上一题类似的思想。也是设置两个指针，只不过这里是，两个指针同
	时向前走，前面的指针每次走两步，后面的指针每次走一步，前面的指针走到最后一个
	结点时，后面的指针所指结点就是中间结点，即第(n/2+1)个结点。注意链表为空，
	链表结点个数为1和2的情况。时间复杂度O(n)。
	*/

	// 获取单链表中间结点，若链表长度为n(n>0)，则返回第n/2+1个结点
	ListNode * GetMiddleNode(ListNode * pHead)
	{
		// 链表为空或只有一个结点，返回头指针
		if(pHead == NULL || pHead->m_pNext == NULL) 
			return pHead;

		ListNode * pAhead = pHead;
		ListNode * pBehind = pHead;

		// 前面指针每次走两步，直到指向最后一个结点，后面指针每次走一步
		while(pAhead->m_pNext != NULL) 
		{
			pAhead = pAhead->m_pNext;
			pBehind = pBehind->m_pNext;
			if(pAhead->m_pNext != NULL)
				pAhead = pAhead->m_pNext;
		}

		// 后面的指针所指结点即为中间结点
		return pBehind; 
	}

### 7. 判断单链表是否有环

	/* 这里也是用到两个指针。如果一个链表中有环，也就是说用一个指针去遍历，是永远走不到头的。
	因此，我们可以用两个指针去遍历，一个指针一次走两步，一个指针一次走一步，如果有环，两个指
	针肯定会在环中相遇。时间复杂度为O(n)。
	*/

	bool HasCircle(ListNode * pHead)
	{
		ListNode * pFast = pHead; // 快指针每次前进两步
		ListNode * pSlow = pHead; // 慢指针每次前进一步
		while(pFast != NULL && pFast->m_pNext != NULL)
		{
			pFast = pFast->m_pNext->m_pNext;
			pSlow = pSlow->m_pNext;

			// 相遇，存在环
			if(pSlow == pFast) 
				return true;
		}
		return false;
	}

### 8. 合并两个排序的链表

	/* 类似归并排序,尤其注意两个链表都为空，和其中一个为空时的情况 */

	ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
    {
        if(pHead1 == NULL)
            return pHead2;
        else if(pHead2 == NULL)
            return pHead1;

        ListNode* pMergedHead = NULL;

        if(pHead1->m_nValue < pHead2->m_nValue)
        {
            pMergedHead = pHead1;
            pMergedHead->m_pNext = Merge(pHead1->m_pNext, pHead2);
        }
        else
        {
            pMergedHead = pHead2;
            pMergedHead->m_pNext = Merge(pHead1, pHead2->m_pNext);
        }

        return pMergedHead;
    }

### 9. 复杂链表的复制

	/* 在复制链表中，每个结点除了有一个m_pNext指针指向下一个结点外，还有一个m_pSibling
	指向链表中的任意结点或者NULL
	*/

	// 第一步，根据原始链表的每个结点N创建对应的N'
	void CloneNodes(ComplexListNode* pHead);

	// 第二步，设置复制出来的结点的m_pSibling
	void ConnectSiblingNodes(ComplexListNode* pHead);

	// 第三步，把长链表拆分成两个链表
	ComplexListNode* ReconnectNodes(ComplexListNode* pHead);

	ComplexListNode* Clone(ComplexListNode* pHead)
	{
	    CloneNodes(pHead);
	    ConnectSiblingNodes(pHead);
	    return ReconnectNodes(pHead);
	}

	void CloneNodes(ComplexListNode* pHead)
	{
	    ComplexListNode* pNode = pHead;
	    while(pNode != NULL)
	    {
	        ComplexListNode* pCloned = new ComplexListNode();
	        pCloned->m_nValue = pNode->m_nValue;
	        pCloned->m_pNext = pNode->m_pNext;
	        pCloned->m_pSibling = NULL;
	 
	        pNode->m_pNext = pCloned;
	 
	        pNode = pCloned->m_pNext;
	    }
	}

	void ConnectSiblingNodes(ComplexListNode* pHead)
	{
	    ComplexListNode* pNode = pHead;
	    while(pNode != NULL)
	    {
	        ComplexListNode* pCloned = pNode->m_pNext;
	        if(pNode->m_pSibling != NULL)
	        {
	            pCloned->m_pSibling = pNode->m_pSibling->m_pNext;
	        }
	 
	        pNode = pCloned->m_pNext;
	    }
	}

	ComplexListNode* ReconnectNodes(ComplexListNode* pHead)
	{
	    ComplexListNode* pNode = pHead;
	    ComplexListNode* pClonedHead = NULL;
	    ComplexListNode* pClonedNode = NULL;
	 
	    if(pNode != NULL)
	    {
	        pClonedHead = pClonedNode = pNode->m_pNext;
	        pNode->m_pNext = pClonedNode->m_pNext;
	        pNode = pNode->m_pNext;
	    }
	 
	    while(pNode != NULL)
	    {
	        pClonedNode->m_pNext = pNode->m_pNext;
	        pClonedNode = pClonedNode->m_pNext;
	 
	        pNode->m_pNext = pClonedNode->m_pNext;
	        pNode = pNode->m_pNext;
	    }
	 
	    return pClonedHead;
	}

### 10. 判断两个单链表是否相交

	/* 如果两个链表相交于某一节点，那么在这个相交节点之后的所有节点都是两个链表所共有的。也就是
	说，如果两个链表相交，那么最后一个节点肯定是共有的。先遍历第一个链表，记住最后一个节点，然后
	遍历第二个链表，到最后一个节点时和第一个链表的最后一个节点做比较，如果相同，则相交，否则不相
	交。时间复杂度为O(len1+len2)，因为只需要一个额外指针保存最后一个节点地址，空间复杂度为O(1)。
	*/

	bool IsIntersected(ListNode * pHead1, ListNode * pHead2)
	{
        if(pHead1 == NULL || pHead2 == NULL)
                return false;

		ListNode * pTail1 = pHead1;
		while(pTail1->m_pNext != NULL)
			pTail1 = pTail1->m_pNext;

		ListNode * pTail2 = pHead2;
		while(pTail2->m_pNext != NULL)
			pTail2 = pTail2->m_pNext;

		return pTail1 == pTail2;
	}

### 11. 求两个链表的第一个公共结点
	
	/* 首先遍历两个链表得到它们的长度，就能知道哪个链表比较长，以及长的链表比短的链表多几个结点。
	在第二次遍历的时候，在较长的链表上先走若干步，接着再同时在两个链表上遍历，找到的第一个相同的
	结点就是它们的第一个公共结点。
	*/

	unsigned int GetListLength(ListNode* pHead);

    ListNode* FindFirstCommonNode( ListNode *pHead1, ListNode *pHead2)
    {
        // 得到两个链表的长度
        unsigned int nLength1 = GetListLength(pHead1);
        unsigned int nLength2 = GetListLength(pHead2);
        int nLengthDif = nLength1 - nLength2;
     
        ListNode* pListHeadLong = pHead1;
        ListNode* pListHeadShort = pHead2;
        if(nLength2 > nLength1)
        {
            pListHeadLong = pHead2;
            pListHeadShort = pHead1;
            nLengthDif = nLength2 - nLength1;
        }
     
        // 先在长链表上走几步，再同时在两个链表上遍历
        for(int i = 0; i < nLengthDif; ++ i)
            pListHeadLong = pListHeadLong->m_pNext;
     
        while((pListHeadLong != NULL) && (pListHeadShort != NULL) &&
            (pListHeadLong != pListHeadShort))
        {
            pListHeadLong = pListHeadLong->m_pNext;
            pListHeadShort = pListHeadShort->m_pNext;
        }
     
        // 得到第一个公共结点
        ListNode* pFisrtCommonNode = pListHeadLong;
     
        return pFisrtCommonNode;
    }

    unsigned int GetListLength(ListNode* pHead)
    {
        unsigned int nLength = 0;
        ListNode* pNode = pHead;
        while(pNode != NULL)
        {
            ++ nLength;
            pNode = pNode->m_pNext;
        }
     
        return nLength;
    }

### 12. 已知单链表存在环，求进入环中的第一个结点

	/* 首先判断是否存在环,若不存在结束。在环中的一个节点处断开(当然函数结束时不能破坏原链表),
	这样就形成了两个相交的单链表,求进入环中的第一个节点也就转换成了求两个单链表相交的第一个节点。

	ListNode* GetFirstNodeInCircle(ListNode * pHead)
	{
		if(pHead == NULL || pHead->m_pNext == NULL)
			return NULL;

		ListNode *pFast = pHead;
		ListNode *pSlow = pHead;
		while(pFast != NULL && pFast->m_pNext != NULL)
		{
			pSlow = pSlow->m_pNext;
			pFast = pFast->m_pNext->m_pNext;
			if(pSlow == pFast)
				break;
		}
		if(pFast == NULL || pFast->m_pNext == NULL)
			return NULL;

		// 将环中的此节点作为假设的尾节点，将它变成两个单链表相交问题
		ListNode *pAssumedTail = pSlow; 
		ListNode *pHead1 = pHead;
		ListNode *pHead2 = pAssumedTail->m_pNext;

		ListNode *pNode1, *pNode2;
		int len1 = 1;
		ListNode * pNode1 = pHead1;
		while(pNode1 != pAssumedTail)
		{
			pNode1 = pNode1->m_pNext;
			len1++;
		}
		
		int len2 = 1;
		ListNode *pNode2 = pHead2;
		while(pNode2 != pAssumedTail)
		{
			pNode2 = pNode2->m_pNext;
			len2++;
		}

		pNode1 = pHead1;
		pNode2 = pHead2;

		// 先对齐两个链表的当前结点，使之到尾节点的距离相等
		if(len1 > len2)
		{
			int k = len1 - len2;
			while(k--)
				pNode1 = pNode1->m_pNext;
		}
		else
		{
			int k = len2 - len1;
			while(k--)
				pNode2 = pNode2->m_pNext;
		}
		while(pNode1 != pNode2)
		{
			pNode1 = pNode1->m_pNext;
			pNode2 = pNode2->m_pNext;
		}
	    return pNode1;
	}








































