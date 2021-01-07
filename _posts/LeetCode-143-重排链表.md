---
title: LeetCode-143-重排链表
date: 2020-10-20 18:31:21
tags:
- LeetCode
- 算法
categories:
- LeetCode
- 算法
---



给定一个单链表 L：L0→L1→…→Ln-1→Ln ，
将其重新排列后变为： L0→Ln→L1→Ln-1→L2→Ln-2→…

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

<!--more -->

示例1：

```
给定链表 1->2->3->4, 重新排列为 1->4->2->3.
```

实例2：

```
给定链表 1->2->3->4->5, 重新排列为 1->5->2->4->3.
```



解题思路：

如果是直接去把L~n~取出来添加到L~1~下，不仅第一次需要遍历整个链表，第二次还需要遍历，很麻烦，很浪费时间。

我们不如直接把整个链表遍历一遍，放在List里面（跟数组一样），然后定义两个整数，一个在前面，一个在后面，把后面的数添加到前面的数的后面，然后前面的加，后面的减。直到最后。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
     
     public void reorderList(ListNode head) {
    if (head == null) {
        return;
    }
    //存到 list 中去
    List<ListNode> list = new ArrayList<>();
    while (head != null) {
        list.add(head);
        head = head.next;
    }
    //头尾指针依次取元素
    int i = 0, j = list.size() - 1;
    while (i < j) {
        list.get(i).next = list.get(j);
        i++;
        //偶数个节点的情况，会提前相遇
        if (i == j) {
            break;
        }
        list.get(j).next = list.get(i);
        j--;
    }
    list.get(i).next = null;
  }

}
```

**复杂度分析**

- 时间复杂度：O(N)*O*(*N*)，其中 N*N* 是链表中的节点数。
- 空间复杂度：O(N)*O*(*N*)，其中 N*N* 是链表中的节点数。主要为线性表的开销。