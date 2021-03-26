# 链表
LeetCode当中，链表的题目大多是单链表（single-linked list），故下面着重介绍单链表
# 单链表
## java语言定义：  

      public class ListNode {
            int val;
            ListNode next;
            ListNode() {}
            ListNode(int val) { this.val = val; }
            ListNode(int val, ListNode next) { this.val = val; this.next = next; }
      }
      
## 基本操作
### 结点的插入

      public void insertNode(ListNode head, ListNode ins) {//head为要插入位置的前一个结点
            ListNode temp = head.next;
            head.next = ins;
            ins.next = temp
      }  
      
### 结点的删除

      public void deletNode(ListNode head) {//head为要删除位置的前一个结点
            head.next = head.next.next
      }

## 刷题常见套路
### 双指针
#### 一次遍历找到链表中点

      // 若链表长度为n(n > 1)，则返回第Math.ceil(n/2);若为1或空，则返回head
      public ListNode findMid(ListNode head) {
            if(head == null || head.next == null) return head;
            ListNode slow = head, fast = head;
            while(fast.next != null and fast.next.next != null) {
                  slow = slow.next;
                  fast = fast.next.next;
            }
            return slow;
      }

可用于O(1)空间复杂度判断回文链表 [234.回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)  

#### 判断链表是否有环
算法：Floyd判圈法，由称龟兔赛跑算法。[wiki链接](https://zh.wikipedia.org/wiki/Floyd%E5%88%A4%E5%9C%88%E7%AE%97%E6%B3%95)  
若链表中存在环，那么以不同速度前进的两个指针必定在某个时刻相遇；
若指针从同一起点开始(如head)，那么不仅可以判断环，而且可以判断环的起点和长度。  

数学证明：  
设链表头到环头的距离为m，环的长度为n；第一次相遇时距离环头k
slow指针每次走1步，fast指针每次走两步
那么slow指针移动距离为 i = m + k + a * n，(a 为慢指针绕环圈数)
则fast为 2i = m + k + b * n (b 为快指针绕环圈数)
i = 2i - i = (b - a)n，为圈数的整数倍。

将其中一个指针(不妨为slow)放到链头，两指针以相同速度前进，当前进m步时，slow距离链头m,fast距离链头i + m,i 为圈的整数倍，故slow和fast再次相遇，相遇的位置即为环的起点。  
将其中一个指针原地不动，另一指针(不妨为slow)以速度1前进，当再次相遇时，slow移动的距离即为环的长度。  




      

            
