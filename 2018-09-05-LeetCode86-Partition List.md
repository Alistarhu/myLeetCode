# 86. Partition List - Medium

## Description
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

## Example
```
Input: head = 1->4->3->2->5->2, x = 3
Output: 1->2->2->4->3->5
```

## Analysis
这道题需要按照给定的某个值作为分界点对链表进行分隔排序，主要考察指针的相关操作。

这里使用最常规的思路：使用两个指针分别维护两个子链表(小于该数字、大于该数字的链表)，最后将两个链表进行拼接。

**这里有几点需要注意**
- 排在后面的(大于该数字)子链表中最后一个元素应该与原链表断开连接，重新指向NULL，表示末尾
- 需要考虑到前后两个子链表是否为空情况下的处理

## Solution
```
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
    ListNode* partition(ListNode* head, int x) {
        ListNode* smallHead=NULL;
        ListNode* smallList=NULL;
        ListNode* bigHead=NULL;
        ListNode* bigList=NULL;
        if(head==NULL)
            return NULL;
        ListNode* curNode=head;
        while(curNode)
        {
            if(curNode->val<x)
            {
                if(smallHead==NULL)
                {
                    smallHead=curNode;
                    smallList=curNode;
                }
                else
                {
                    smallList->next=curNode;
                    smallList=smallList->next;
                }
            }
            else
            {
                if(bigHead==NULL)
                {
                    bigHead=curNode;
                    bigList=curNode;
                }
                else
                {
                    bigList->next=curNode;
                    bigList=bigList->next;
                }
            }
            curNode=curNode->next;
        }
        // deal with the last element !!!
        if(bigList!=NULL)
            bigList->next=NULL;
        if(smallHead!=NULL)
        {
            smallList->next=bigHead;
            return smallHead;
        }  
        else
            return bigHead;
    }
};
```
