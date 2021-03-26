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
      
## 常用操作
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

### 反转链表
很简单，cur.next = pre即可。但问题是，单链表没有前指针，怎么找到'pre'，以及改变cur.next之后，如何找到原本的cur.next，并重复上述操作cur.next = pre。  
这就需要我们把pre和next分别存储起来。

      public ListNode reverseList(ListNode head) {
            ListNode pre = null;
            ListNode cur = head;
            ListNode nex = null;
            while(cur != null) {
                  nex = cur.next;
                  cur.next = pre;
                  pre = cur;
                  cur = nex;
            }
            return head;
      }

更进一步，只反转链表中的m到n号结点呢？（值得注意的是，m = 1 或 n = length 的边界条件）  
[206.反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)   
[92.反转链表ii](https://leetcode-cn.com/problems/reverse-linked-list-ii/) 
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
  
[234.回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)  
[143. 重排链表](https://leetcode-cn.com/problems/reorder-list/)  
[148. 排序链表（归并排序）](https://leetcode-cn.com/problems/sort-list/)   
#### 判断链表是否有环
算法：Floyd判圈法，由称龟兔赛跑算法。[wiki链接](https://zh.wikipedia.org/wiki/Floyd%E5%88%A4%E5%9C%88%E7%AE%97%E6%B3%95)  
若链表中存在环，那么以不同速度前进的两个指针必定在某个时刻相遇；
若指针从同一起点开始(如head)，那么不仅可以判断环，而且可以判断环的起点和长度。  

数学证明：  
设链表头到环头的距离为m，环的长度为n；第一次相遇时距离环头k。  
slow指针每次走1步，fast指针每次走两步。  
那么slow指针移动距离为 i = m + k + a * n，(a 为慢指针绕环圈数)  
则fast为 2i = m + k + b * n (b 为快指针绕环圈数)  
i = 2i - i = (b - a)n，为圈数的整数倍。  

将其中一个指针(不妨为slow)放到链头，两指针以相同速度前进，当前进m步时，slow距离链头m,fast距离链头i + m,i 为圈的整数倍，故slow和fast再次相遇，相遇的位置即为环的起点。  
将其中一个指针原地不动，另一指针(不妨为slow)以速度1前进，当再次相遇时，slow移动的距离即为环的长度。  

      int m = 0;//环起始位置
      int n = 0;//环长
      public boolean hasCycle(ListNode head) {
            if(head == null || head.next == null) return false;
            ListNode slow = head, fast = head;
            do{
                  if(fast == null || fast.next == null) return false;
                  slow = slow.next;
                  fast = fast.next.next;
               }while(slow != fast);
            
            do{
                  slow = slow.next;
                  m++;
               }while(slow != fast);
               
            slow = head;
            do{
                  slow = slow.next;
                  fast = fast.next;
                  n++;
               }while(slow != fast);
            return true;
         }

[141.环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)  
[142.环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)  
### dummyNode
不多解释，看题就明白了
[82. 删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)  
[21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists)
[86. 分隔链表](https://leetcode-cn.com/problems/partition-list/)  

### 以空间换时间
有些时候，链表不能随机访问，操作不便，我们可以用空间换时间，如在[234.回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)中，将链表转存到数组中，再判断，就会容易很多（虽然不是最优解法）
或者，在单个链表中操作不便，可以使用多个链表存储数据，如[86. 分隔链表](https://leetcode-cn.com/problems/partition-list/)  
            


      

            
