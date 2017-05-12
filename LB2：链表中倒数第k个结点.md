### 题目：输入一个链表，输出该链表中倒数第k个结点。（k从1开始）
思路：所谓输入一个链表是指输入一个头结点这个输入的结点必然是含有next指针的对象，于是之后的多个结点相互连接形成一个链表。
倒数第k个结点，也就正数第k+n-1个结点，只需要遍历链表，返回第k+n-1个结点即可；但是此时由于n是不知道的，为了得到n需要先遍历一遍链表，然后再从头到尾遍历到第k+n-1个元素，这样就需要遍历2次链表，效率较差；与之类似的还有使用栈Stack,也需要先将所有结点全部放入栈中并得到n,然后再逐个谈栈得到第k+n-1个元素，也需要遍历2次链表；
最佳思路是：只遍历一次链表就可以确定倒数第k个结点；使用两个指针ppre，plast分别表示前后两个当前结点指针（按照遍历方向在前的是pre,再后面的是last）；这两个指针的距离保持为k-1,首先plast指针不动，ppre指针向前遍历k-1个结点，然后plast指针开始一起移动，当ppre指针指向最后一个结点时，plast指针所指向的结点就是第n+k-1个结点，即倒数第k个结点。
鲁棒性：几个bug需要注意并排除：
* 1.当输入的链表头结点是null时，应该直接返回null；
* 2.当输入的k是0时，直接返回null；
* 3.当k比整个链表的元素还要多时，直接返回null；


```java
//对于特殊的输入和特殊情况一定要做处理，否则无法通过相应得测试用例
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        //定义两个指针
        ListNode ppre=head;
        ListNode plast=head;
        //鲁棒性：输入值要符合要求
        if(k<=0||head==null){
           return null;
        }   
        //指针ppre先走k-1
        for(int i=1;i<=k-1;i++){
            ppre=ppre.next;
            //保证k不超出n
           if(ppre==null){
                return null;
           }
        }
        //两个指针一起走，直到ppre指向尾结点
        while(ppre.next!=null){
            ppre=ppre.next;
            plast=plast.next;
        }
        //此时返回plast即为倒数第k个结点
        return plast;
    }
}
```
