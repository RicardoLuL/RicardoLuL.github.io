# [剑指offer](https://www.nowcoder.com/exam/oj/ta?page=1&tpId=13&type=13)
## 链表
* 包含环的
  * [链表中是否有环](https://www.nowcoder.com/practice/650474f313294468a4ded3ce0f7898b9?tpId=295&tqId=40164&rp=1&ru=/ta/format-top101&qru=/ta/format-top101&difficulty=&judgeStatus=&tags=/question-ranking)
  * [链表环入口在哪里](https://www.nowcoder.com/practice/253d2c59ec3e4bc68da16833f79a38e4?tpId=13&tqId=23449&ru=%2Fpractice%2F253d2c59ec3e4bc68da16833f79a38e4&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&sourceUrl=%2Fexam%2Foj%2Fta%3Fpage%3D1%26tpId%3D13%26type%3D13)
> [!NOTE]
> 1. 有环就用双指针 快+慢 : 快指针（2步, fast.next.next）和慢指针（1步, low.next）同时从链表头出发。如果循环到没有next，就说明没有环；如果循环到fast==low，就说明有环。
> 2. 用哈希存储 ：遍历链表，每个元素存入哈希表中，每次循环判断是否在哈希表，在的话就有环，不在就添加进去add
> 1. 快慢指针：**STEP1**，判断是否有环，有环返回相遇节点（fast==slow），无环返回None；**STEP2**：获得相遇节点后，fast从链表头开始，slow从相遇节点开始，两者一定在环入口处相遇，返回环入口节点。
> 2. 哈希表

* 双指针类型：
  两个指针或是同方向访问两个链表、或是同方向访问一个链表（快慢指针）、或是相反方向扫描（对撞指针、回文串）

*  删除链表中重复的结点
````
# 牛客题解很繁琐，这里如果有重复直接下一个，pre相应链到下一个节点上，最后返回头节点即可
def deleteDuplication(self , pHead: ListNode) -> ListNode:
        # write code here
        cur = pHead
        pre = ListNode(None)
        pre.next = pHead
        res = pre 
        while cur and cur.next:
            if cur.val == cur.next.val:
                temp = cur.val
                while cur and cur.val == temp:
                    cur = cur.next
                    pre.next = cur
            else:
                pre = cur
                cur = cur.next
        return res.next
````

* 复杂链表的复制 涉及next和random指针的复制
> [!NOTE]
> 1. 复制链表并插入新节点：将每个新节点插入到原链表的每个节点之后。
>  2. 处理 random 指针：因为新的节点和原节点是成对出现的，所以可以通过调整链表结构来复制 random 指针。
>  3. 拆分链表：将原链表和新链表分离
```
    def Clone(self, pHead):
        # write code here
        if not pHead:
            return None
    
        # Step 1: 复制节点，并将新节点插入到每个原节点的后面
        cur = pHead
        while cur:
            new_node = RandomListNode(cur.label)
            new_node.next = cur.next
            cur.next = new_node
            cur = new_node.next

        
        # Step 2: 复制 random 指针
        cur = pHead
        while cur:
            if cur.random :
                cur.next.random = cur.random.next
            cur = cur.next.next
        
        # Step 3: 拆分链表
        cur = pHead
        clone_head = pHead.next
        while cur:
            clone_node = cur.next
            cur.next = clone_node.next
            if cur.next:
                clone_node.next = cur.next.next
            cur = cur.next
        return clone_head
```

## 树
[剑指offer](https://www.nowcoder.com/exam/oj/ta?page=1&tpId=13&type=13)
- 二叉搜索树（排序树、查找树）
  - 都是左<根<右，用中序遍历
   
- 二叉树的下一个节点
  > [!NOTE]
  > 1. 有右子树，就找到右子树的最左下节点
  > 2.2 无右子树，但是左节点，找到他的父节点，即next
  > 2.3 无右子树，但是右节点，找到他所在左子树的父节点，或找不到即他只在右子树一堆，返回的就是根节点的next
  >   ![bbd079abe23773281a9b4a5a3e9671b](https://github.com/user-attachments/assets/fb57d8a8-aea1-4acf-979a-9095010a5274)

- 层次遍历
  > 使用队列
  > 1、deque结构 from collections import deque queue = deque() queue.popleft(); 注意每次需要存入树的节点结构，为了下次pop
  > 2、list实现  queue=[root] queue.pop(0)
  > [层次打印二叉树](https://www.nowcoder.com/practice/7fe2212963db4790b57431d9ed259701?tpId=13&tqId=23280&ru=/exam/oj/ta&qru=/ta/coding-interviews/question-ranking&sourceUrl=%2Fexam%2Foj%2Fta%3Fpage%3D1%26tpId%3D13%26type%3D13)
[模板速刷101](https://www.nowcoder.com/ta/format-top101)




