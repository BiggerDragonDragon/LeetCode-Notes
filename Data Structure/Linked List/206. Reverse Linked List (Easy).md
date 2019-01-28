## [206 Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) (Easy)

Reverse a singly linked list.

**Example:**

```c++
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

**Follow up:**

A linked list can be reversed either iteratively or recursively. Could you implement both?



## Solution (C++)

------

#### Approach #1 (Iterative) [Accepted] [100%]

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
    ListNode* reverseList(ListNode* head) {
        ListNode *newHead = NULL;
        while(head)
        {
            ListNode *headNext = head->next;
            head->next = newHead;
            newHead = head;
            head = headNext;
        }
        return newHead;
    }
};
```

**Complexity analysis**

- Time complexity : O(n). Assume that n is the list's length, the time complexity is O(n).
- Space complexity : O(1)

---

#### Approach #2 (Iterative) [Accepted] [100%]

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *prev = NULL;
        ListNode *curr = head;
        while(curr)
        {
            ListNode *next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;            
        }
        return prev;
    }
};
```

**Complexity analysis**

- Time complexity : O(n). Assume that n is the list's length, the time complexity is O(n).
- Space complexity : O(1)

---

#### Approach #3 (Recursive) [Accepted] [100%]

```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(!head || !head->next )
            return head;
        else
        {
            ListNode *nextNode = reverseList(head->next);
            head->next->next = head;
            head->next = NULL;   
            return nextNode;
        }
    }
};
```

**Complexity analysis**

- Time complexity : O(n). Assume that n is the list's length, the time complexity is O(n).
- Space complexity : O(n).  The extra space comes from implicit stack space due to recursion. The recursion could go up to n levels deep.

------

## Solution (Python)

------

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Approach #1
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        newHead = None
        while head:
            nextNode = head.next
            head.next = newHead
            newHead = head
            head = nextNode
        return newHead
    
# Approach #2
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        prev = None
        while head:
            nextNode = head.next
            head.next = prev
            prev = head
            head = nextNode
        return prev
    
# Approach #3
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head is None or head.next is None:
            return head
        else:
            nextNode = self.reverseList(head.next)
            head.next.next = head
            head.next = None
            return nextNode
```

