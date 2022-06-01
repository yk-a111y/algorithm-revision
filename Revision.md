## Array

#### properties
  + array.length() => get the size of array
  + array[index] => access element using index

#### basic operations
  + Insertion

  + Deletion

  + linear search (unsorted array)

  + binary search (sorted array, more efficient than linear seaerch)


#### classic problems
  + bubble sort
    ```js
    ```
  + selection sort

  + insertion sort

  + merge-sort
  
  + quick-sort

  + Remove Duplicates from sorted array **(two pointers)**
    ```js
    public int removeDuplicates(int[] nums) {
        int target = 0;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[target]) {
                if (++target != i) {
                    nums[target] = nums[i];
                }
            }
        }
        return target + 1;
    }
    ```

  + merging two sorted arrays **(two pointers)**
    ```js
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int p1 = 0, p2 = 0;
        int[] res = new int[m + n];
        int cur;

        while (p1 < m || p2 < n) {
            if (p1 == m) cur = nums2[p2++];
            else if (p2 == n) cur = nums1[p1++];
            else if (nums1[p1] < nums2[p2]) {
                cur = nums1[p1++];
            } else {
                cur = nums2[p2++];
            }
            res[p1 + p2 - 1] = cur;
        }

        for (int i = 0; i < m + n; i++) {
            nums1[i] = res[i];
        }
    }
    ```

## LLD

#### properties
  * header -> node1 -> node2 -> ... -> null
  * node.next => get the next node
  * node.val => get the value of current node

#### basic operations
  + delete node2
    ```js
    // node1 -> node2 -> node3
    node1.next = node3
    // delete header
    header = header.next
    ```
  + insertion
    ```js
    // preNode insertNode and curNode
    // preNode -> (insertNode)-> curNode
    preNode.next = insertNode
    insertNode.next = curNode
    ```

#### classic problems
  * design linked-list
    ```js
    class ListNode {
      int val;
      ListNode next;
      ListNode(int x) { val = x; }
    }

    class MyLinkedList {

      int size = 0;
      ListNode head;;

      public MyLinkedList() {
          size = 0;
          head = new ListNode(0);
      }
      
      public int get(int index) {
          if (index < 0 || index >= size) return -1;

          ListNode cur = head;
          for (int i = 0; i < index + 1; i++) {
              cur = cur.next;
          }
          return cur.val;
      }
      
      public void addAtHead(int val) {
          addAtIndex(0, val);
      }
      
      public void addAtTail(int val) {
          addAtIndex(size, val);
      }
      
      public void addAtIndex(int index, int val) {
          if (index > size) return;
          if (index < 0) index = 0;

          ++size;
          ListNode toAdd = new ListNode(val);

          ListNode node = head;
          for (int i = 0; i < index; i++) node = node.next;
          toAdd.next = node.next;
          node.next = toAdd;
      }
      
      public void deleteAtIndex(int index) {
          if (index >= size || index < 0) return;
          size--;
          ListNode node = head;
          for (int i = 0; i < index; i++) {
              node = node.next;
          }
          node.next = node.next.next;
      }
    }
    ```
  * linked list cycle
    ```js
    public boolean hasCycle(ListNode head) {
        if (head == null) {
            return false;
        }
        ListNode slow = head;
        ListNode fast = head.next;

        while (fast != null && fast.next != null) {
            if (fast == slow) {
                return true;
            }
            slow = slow.next;
            fast = fast.next.next;
        }
        return false;
    }
    ```
  * intersection of two linked-list
    ```js
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }
        ListNode a = headA, b = headB;
        while (a != b) {
            a = a == null ? headB : a.next;
            b = b == null ? headA : b.next;
        }
        return a;
    }
    ```
  * reverse linked list
    ```js
    public ListNode reverseList(ListNode head) {
        ListNode node = head;
        ListNode pre = null;
        while (node != null) {
            ListNode next = node.next;
            node.next = pre;
            pre = node;
            node = next;;
        }
        return pre;
    }
    ```

## Stack

#### properties
  * first-in-last-out(FILO)
  * stack.push(x) => push the element into stack
  * stack.pop() => delete the element at the top of stack
  * stack.peek() => get the element at the top of stack
  * stack.size() => size of stack
  * stack.isEmpty() => if stack is empty return true
  * stack.clear() => clear the stack
  
#### classic problems
  * well-bracked 有效括号
    ```js
    public boolean isValid(String s) {
      Stack<Character> stack = new Stack<>();
      char[] chars = s.toCharArray();
      for (char c : chars) {
          if (c == '(') stack.push(')');
          else if (c == '[') stack.push(']');
          else if (c == '{') stack.push('}');
          else if (stack.isEmpty() || c != stack.pop()) return false;
      }
      return stack.isEmpty();
    }
    ```
  * implementation queue using stack 栈实现队列
    ```js
    class MyQueue {
      private Stack<Integer> s1;
      private Stack<Integer> s2;
      public MyQueue() {
          s1 = new Stack<>();
          s2 = new Stack<>();
      }

      public void push(int x) {
          s1.push(x);
      }

      public int pop() {
          if (s2.isEmpty()) {
              while (!s1.isEmpty()) {
                  s2.push(s1.pop());
              }
          }
          if (!s2.isEmpty()) {
              return s2.pop();
          }
          return -1;
      }

      public int peek() {
          if (s2.isEmpty()) {
              while (!s1.isEmpty()) {
                  s2.push(s1.pop());
              }
          }
          if (!s2.isEmpty()) {
              return s2.peek();
          }
          return -1;
      }

      public boolean empty() {
          if (s1.isEmpty() && s2.isEmpty()) {
              return true;
          }
          return false;
      }
    }
    ```
  * 老鼠迷宫
  * get the least element in stack with time complexity O(1)
    ```js
    class MinStack {

      Stack<Integer> xStack;
      Stack<Integer> minStack;

      public MinStack() {
          xStack = new Stack<>();
          minStack = new Stack<>();
          minStack.push(Integer.MAX_VALUE);
      }
      
      public void push(int val) {
          xStack.push(val);
          minStack.push(minStack.peek() < val ? minStack.peek() : val);
      }
      
      public void pop() {
          xStack.pop();
          minStack.pop();
      }
      
      public int top() {
          return xStack.peek();
      }
      
      public int getMin() {
          return minStack.peek();
      }
    }
    ```
  * Trapping rain water (Leetcode-42 **difficult**)
    ```js
    public int trap(int[] height) {
        int res = 0;
        Stack<Integer> s = new Stack<>();
        for (int i = 0; i < height.length; i++) {
            while (!s.isEmpty() && height[s.peek()] < height[i]) {
                int cur = s.pop();
                while (!s.isEmpty() && height[s.peek()] == height[cur]) {
                    s.pop();
                }
                if (!s.isEmpty()) {
                    int sTop = s.peek();
                    res += (Math.min(height[sTop], height[i]) - height[cur]) * (i - sTop - 1);
                }
            }
            s.push(i);
        }
        return res;
    }
    ```

## Set

#### properties

## Map

#### properties

## Binary Tree

#### properties

## Hash

#### properties