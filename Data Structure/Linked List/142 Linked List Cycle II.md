## [142 Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) (Medium)

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

**Note:** Do not modify the linked list.

 

**Example 1:**

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Example 2:**

```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Example 3:**

```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

 

**Follow up**:
 Can you solve it without using extra space?

## Solution (C++)

------

#### Approach #1  [Accepted] [16.67%] (set)

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
    ListNode *detectCycle(ListNode *head) {
        set <ListNode*> NodeSet;
        while(head)
        {
            if(NodeSet.find(head)!=NodeSet.end())
                return head;
            NodeSet.insert(head);
            head = head->next;
        }
        return NULL;
    }
};
```

**Complexity analysis**

- Time complexity : O(n^2). Assume that n is the list's length, the time complexity is O(n).
- Space complexity : O(n)

------

#### Approach #2 [Accepted] [100%] (Two Pointer)

```c++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode * SlowNode = head;
        ListNode * FastNode = head;
        while(FastNode)
        {
            if(!FastNode->next || ! FastNode->next->next)
                return NULL;
            SlowNode = SlowNode->next;
            FastNode = FastNode->next->next;
            if(FastNode == SlowNode)
                break;
        }
        while(head != SlowNode)
        {
            head = head->next;
            SlowNode = SlowNode->next;
        }
        return head;
    }
};
```

**Complexity analysis**

- Time complexity : O(n). Assume that n is the list's length, the time complexity is O(n).
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
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        FastNode = head
        SlowNode = head
        while(FastNode):
            if(FastNode.next is None or FastNode.next.next is None):
                return None
            FastNode = FastNode.next.next
            SlowNode = SlowNode.next
            if(FastNode == SlowNode):
                break
        while(head != SlowNode):
            SlowNode = SlowNode.next
            head = head.next
        return head
```

