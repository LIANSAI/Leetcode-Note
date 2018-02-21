# Tags Linked List -easy

---

21 Merge Two Sorted List

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        dummy = cur =ListNode(0)
        while l1 and l2:
            if l1.val <l2.val:
                cur.next = l1
                l1 = l1.next
            else:
                cur.next= l2
                l2=l2.next

            cur = cur.next

        cur.next = l1 or l2 

        return dummy.next #加next为了不包括0节点
```

---

83 Remove duplicates from Sorted LIst

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        current = head
        while current is not None:
            while current.next and current.next.val == current.val:
                current.next = current.next.next

            current=current.next

        return head
```

---

141 Listed Cycle

类似长跑中的套圈

```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        fast=slow=head

        while fast and fast.next:
            slow=slow.next
            fast=fast.next.next
            if slow==fast:
                return True
        return False
```

---

160 Inserction of Two list

```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):


        pa = headA # 2 pointers
        pb = headB

        while pa is not pb:
            # if either pointer hits the end, switch head and continue the second traversal, 
            # if not hit the end, just move on to next
            pa = headB if pa is None else pa.next
            pb = headA if pb is None else pb.next

        return pa
```

---

203 Remove elements from List

```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        head,head.next=ListNode(0),head  #可能会出现空集合【】

        cur=head   
        while cur.next:
            if cur.next.val == val:
                cur.next=cur.next.next

            else: cur = cur.next

        return head.next
```



