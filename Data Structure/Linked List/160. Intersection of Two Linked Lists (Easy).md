## [160 Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/) (Easy)

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

![img](https://assets.leetcode.com/uploads/2018/12/13/160_statement.png)

begin to intersect at node c1.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
Output: Reference of the node with value = 8
Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

 

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

```
Input: intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
Output: Reference of the node with value = 2
Input Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [0,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
```

 

**Example 3:**

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)

```
Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: null
Input Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
```

 

**Notes:**

- If the two linked lists have no intersection at all, return `null`.
- The linked lists must retain their original structure after the function returns.
- You may assume there are no cycles anywhere in the entire linked structure.
- Your code should preferably run in O(n) time and use only O(1) memory.

## Solution (C++)

------

#### Approach #1  [Accepted] [18.04%]

```c++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if(!headA || !headB)
            return NULL;
        vector<ListNode*> arrayA;
        vector<ListNode*> arrayB;
        while(headA)
        {
            arrayA.push_back(headA);
            headA = headA->next;
        }
        while(headB)
        {
            arrayB.push_back(headB);
            headB = headB->next;
        }
        int lenA = arrayA.size();
        int lenB = arrayB.size();
        if(arrayA[lenA - 1] != arrayB[lenB - 1])
            return NULL;
        for (int i = lenA - 2, j = lenB - 2; i >= 0 && j >= 0 ; i--, j--)
        {
            if(arrayA[i] != arrayB[j])
                return arrayA[i + 1];
        }
        if(lenA < lenB)
            return arrayA[0];
        return arrayB[0];
    }
};
```

**Complexity analysis**

- Time complexity : O(nlogn). Assume that n is the list's length, the time complexity is O(n).
- Space complexity : O(n)

------

#### Approach #2 [Accepted] [12.37%]

```c++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        set<ListNode *> NodeSet;
        while(headA)
        {
            NodeSet.insert(headA);
            headA = headA->next;
        }
        while(headB)
        {
            if(NodeSet.find(headB)!=NodeSet.end())
                return headB;
            headB = headB->next;   
        }
        return NULL;
    }
};
```

**Complexity analysis**

- Time complexity : O(nlogn). Assume that n is the list's length, the time complexity is O(n).
- Space complexity : O(n). 

------

#### Approach #3 [Accepted] [95.36%] (Two Pointer)

```c++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode * StartA = headA;
        ListNode * StartB = headB;
        int lenA = 0, lenB = 0;
        while(StartA)
        {
            lenA++;
            StartA = StartA->next;
        }
        while(StartB)
        {
            lenB++;
            StartB = StartB->next;
        }
        ListNode * shortList = NULL;
        ListNode * longList = NULL;
        int diffNum = 0;
        if (lenA <= lenB)
        {
            diffNum = lenB - lenA;
            shortList = headA;
            longList = headB;
        }
        else
        {
            diffNum = lenA - lenB;
            shortList = headB;
            longList = headA;
        }
        while(diffNum--)
        {
            longList = longList->next;
        }
        while(longList != shortList)
        {
            shortList = shortList->next;
            longList = longList->next;
        }
        return longList;
    }
};
```

**Complexity analysis**

- Time complexity : O(n+m).
- Space complexity : O(1). 

---

## Solution (Python)

------

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        lenA = 0
        lenB = 0
        StartA = headA
        StartB = headB
        while(StartA):
            lenA += 1
            StartA = StartA.next
        while(StartB):
            lenB += 1
            StartB = StartB.next
        if(lenA >= lenB):
            Diff = lenA - lenB
            StartA = headA
            StartB = headB
            while(Diff):
                StartA =StartA.next
                Diff -= 1
        else:
            Diff = lenB - lenA
            StartA = headA
            StartB = headB
            while(Diff):
                StartB =StartB.next    
                Diff -= 1
        while(StartA):
            if(StartA == StartB):
                return StartA
            StartA = StartA.next
            StartB = StartB.next
        return None
```

