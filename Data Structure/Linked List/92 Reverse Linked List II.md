## [92 Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/) (Medium)

Reverse a linked list from position *m* to *n*. Do it in one-pass.

**Note:** 1 ≤ *m* ≤ *n* ≤ length of list.

**Example:**

```c++
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

## Solution (C++)

------

#### Approach #1 [Accepted] [100%]

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        int numChangeNode = n - m + 1;
        ListNode* Start = head;
        ListNode* preHead = NULL;
        while(head && --m)
        {
            preHead = head;
            head = head->next;
        }
        ListNode* LastNodeAfterReverse = head;
        ListNode* prev = NULL;
        ListNode* next = head;
        while(numChangeNode--)
        {
            head = next;
            next = head->next;
            head->next = prev;
            prev = head;
        }
        LastNodeAfterReverse->next = next;
        if(preHead)
            preHead->next = head;
        else
            Start = head;
        return Start;
               
    }
};
```

**Complexity analysis**

- Time complexity : O(n). Assume that n is the list's length, the time complexity is O(n).
- Space complexity : O(1)

## Solution (Python)

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        start = head
        numChangeNode = n - m + 1
        preHead = None
        m = m - 1
        while(head and m):
            preHead = head
            head = head.next
            m = m - 1
        LastNodeAfterReverse = head
        newHead = None
        nextNode = None
        while(numChangeNode):
            nextNode = head.next
            head.next = newHead
            newHead = head
            head = nextNode
            numChangeNode = numChangeNode - 1
        LastNodeAfterReverse.next = nextNode
        if(preHead):
            preHead.next = newHead
        else:
            start = newHead
        return start
```

