#### 链表练习自测

习题目录：

>[328. 奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/)（中等）
>
>[25. K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)（困难）
>
>[剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)（简单）
>
>[19. 删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)（中等）
>
>[160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)（简单） 
>
>[141. 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)（简单）
>
>[83. 删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)（简单）
>
>[剑指 Offer 25. 合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)（中等）
>
>[2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)（中等）
>
>[206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)（中等）
>
>[234. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)（中等）





[328. 奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/)（中等）

```java
 public ListNode oddEvenList(ListNode head) {
		ListNode oddHead = new ListNode();
		ListNode oddTail = oddHead;
		ListNode evenHead = new ListNode();
		ListNode evenTail = evenHead;
		boolean isEven = true;
		ListNode p = head;
		while (p != null) {
			if (isEven) {
				evenTail.next = p;
				p = evenTail;   
				isEven = false;
			}else {
				oddTail.next = p;
				p = oddTail;
				isEven = true;
			}
			p = p.next;
		}
		evenTail.next = oddHead.next;
		oddTail.next = null;
		return evenHead.next;
    }
```

尾部插入时，p =evenTail 为错误的逻辑，应该为evenTail = p;



[剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)（简单）

```
ListNode fastNode = head;
ListNode slowNode = head;
//  1 2 3 null
for (int i = 0; i < k - 1; i++) {
   if (fastNode == null) {
      return null;
   }
   fastNode = fastNode.next;
}
while (fastNode.next != null) {
   fastNode = fastNode.next;
   slowNode = slowNode.next;
}
return slowNode;
```

直接通过

[19. 删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)（中等）

```
// dummy 1 2 3 null   倒数第2
ListNode dummyNode = new ListNode();
dummyNode.next = head;
// 查找倒数n+1节点
ListNode fastNode = dummyNode;
ListNode slowNode = dummyNode;
// 1 2 3 null
for (int i = 0; i < n; i++) {
   if (fastNode == null) {
      return head;
   }
   fastNode = fastNode.next;
}
while (fastNode.next != null) {
   fastNode = fastNode.next;
   slowNode = slowNode.next;
}
slowNode.next = slowNode.next.next;
return dummyNode.next;
```

直接过



[160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)（简单） 

```
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
   int aLeng = countList(headA);
   int bLeng = countList(headB);
   int diff = aLeng - bLeng;
   ListNode fastNode;
   ListNode anotherNode;
   if(diff < 0) {
      fastNode = headB;
      anotherNode = headA;
      diff = -diff;
   }else {
      fastNode = headA;
      anotherNode = headB;
   }
   for (int i = 0; i < diff; i++) {
      fastNode = fastNode.next;
   }
   while (fastNode != null && anotherNode != null) {
      if (fastNode == anotherNode) {
         return fastNode;
      }
      fastNode = fastNode.next;
      anotherNode = anotherNode.next;
   }
   return null;
   }


private int countList(ListNode head) {
   int i = 0;
   while (head != null) {
      head = head.next;
      i++;
   }
   return i;
}
```

直接过



[141. 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)（简单）

```
public boolean hasCycle(ListNode head) {
if (head == null) {
   return false;
}
ListNode fastNode = head;
ListNode slowNode = head;
while (fastNode.next != null && fastNode.next.next != null) {
   fastNode = fastNode.next.next;
   slowNode = slowNode.next;
   if (fastNode == slowNode) {
      return true;
   }
}
return false;
  }
```



[83. 删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)（简单）

```
 public ListNode deleteDuplicates(ListNode head) {
if (head == null) {
   return null;
}
ListNode p = head;
while (p.next != null) {
   if (p.val == p.next.val) {
      p.next = p.next.next;
   }else{
      p = p.next;
   }
}
return head;
  }
```

[剑指 Offer 25. 合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)（中等）

```java
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
		ListNode dummyNode = new ListNode();
		ListNode p = dummyNode;
		while (l1.next != null || l2.next != null) {
			if (l1.val <= l2.val) {
				p.next = l1;
				l1 = l1.next;
			}else{
				p.next = l2;
				l2 = l2.next;
			}
			p = p.next;
		}
		return dummyNode.next;
    }
```

此版有错