### Definition for singly-linked list.

   class ListNode {  
       int val;  
       ListNode next;  
       ListNode(int x) {  
           val = x;  
           next = null;  
       }
   }  

---

### Explanation
1) минимальные условия, которые говорят о существовании цикла: Должен быть минимум 1 ListNode и минимум 1 next (не null)
2) цикл может начинаться только с последнего элемента
3) если есть цикл, то null у нас не будет
4) быстрый в замкнутом контуре в любом случае догонит более медленного
5) быстрый, находясь впереди никогда не встретится с более медленным, если нет цикла

---

### Code

    public class Solution {
        public boolean hasCycle(ListNode head) {
        // проверка минимальных условий (п.1)
          if (head == null) {
              return false;
          }

          if (head.next == null) {
              return false;
          }

          ListNode slowNode = head;
          ListNode fastNode = head.next.next;

          while (fastNode != null && fastNode.next != null && slowNode != null) {  // если цикл, то никогда не будет равно null
              if (fastNode == slowNode) {
                  return true;   // встретилися, значит есть цикл
              }
              fastNode = fastNode.next.next;
              slowNode = slowNode.next;
          }

          return false;
      }
    }
