# 92. Reverse Linked List II - Medium

## Description
Reverse a linked list from position m to n. Do it in one-pass.

Note: 1 ≤ m ≤ n ≤ length of list.

## Example
```
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

## Analysis
这道题要求对链表中的一段进行翻转，主要考察链表反转操作。由于需要将子链表整体反转，因此需要记录反转子链表起点的上一个节点位置，同时还需考虑到反转的起点为head的情况。

## Solution
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
        ListNode* preNode=NULL;
        ListNode* curNode=head;
        ListNode* startNodePre=NULL;
        if(m==n)
            return head;
        for(int i=1;;i++)
        {
            if(i==m)  // store the start point
            {
                startNodePre=preNode;
                preNode=curNode;
                curNode=curNode->next;
            }
            else if(i>m&&i<n) // reverse each two points
            {
                ListNode* nextNode=curNode->next;
                curNode->next=preNode;
                preNode=curNode;
                curNode=nextNode;
            }
            else if(i==n)
            {
                ListNode* nextNode=curNode->next;
                curNode->next=preNode;
                // reverse the sub-link list, conduct new connect
                if(startNodePre==NULL)
                {
                    head->next=nextNode;
                    head=curNode;
                }
                else
                {
                    startNodePre->next->next=nextNode;
                    startNodePre->next=curNode;
                }
                break;
            }
            else
            {
                preNode=curNode;
                curNode=curNode->next;
            }
        }
        return head;
    }
};
```
