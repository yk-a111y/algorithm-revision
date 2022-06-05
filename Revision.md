## Array
#### properties
  + array.length() => get the size of array
  + array[index] => access element using index

#### basic operations
  + Insertion
    * copy (0, n - 1)
    * array[n] = element

  + Deletion
    * [1, 2, 3, 4, 5] delete 3
    * copy (delPosition + 1, right) to (del, right - 1)：[1, 2, 4, 5, 5]
    * make array[4] unoccupied => [1, 2, 4, 5]

  + linear search (unsorted array)
    ```js
    for (int i = 0; i < len; i++) { 
      if (arr[i] === target) 
      return i
    };
    ```

  + binary search (sorted array, more efficient than linear seaerch)
    ```js
    public int binarySearch(int[] nums, int target) {
        int index = 0, left = 0, right = nums.length - 1;
        while (left <= right) {
            index = left + (right - left) / 2;
            if (nums[index] == target) return index;
            if (nums[index] > target) right = index - 1;
            else left = index + 1;
        }
        return -1;
    }
    ```


#### classic problems
  + bubble sort
    ```js
    public int[] sortArray(int[] nums) {
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            for (int j = 0; j < len - i - 1; j++) {
                if (nums[j] > nums[j + 1]) {
                    int temp = nums[j];
                    nums[j] = nums[j + 1];
                    nums[j + 1] = temp;
                }
            }
        }
        return nums;
    }
    ```
 
  + selection sort
    ```js
    public int[] sortArray(int[] nums) {
        int len = nums.length;

        for (int i = 0; i < len; i++) {
            int min = i;
            for (int j = i + 1; j < len; j++) {
                if (nums[j] < nums[min]) {
                    min = j;
                }
            }
            if (min != i) {
                int temp = nums[i];
                nums[i] = nums[min];
                nums[min] = temp;
            }
        }
        return nums;
    }
    ```

  + insertion sort
    ```js
    public int[] sortArray(int[] nums) {
        int len = nums.length;
        for (int i = 1; i < len; i++) {
            int temp = nums[i];
            for (int j = i - 1; j >= 0; j--) {
                if (nums[j] > temp) {
                    nums[j + 1] = nums[j];
                    if (j == 0) nums[j] = temp;
                } else {
                    nums[j + 1] = temp;
                    break;
                }
            }
        }
        return nums;
    }
    ```

  + merge-sort
    ```js
    public int[] sortArray(int[] nums) {
        if (nums.length <= 1) return nums;
        
        int mid = nums.length / 2;

        int[] left = Arrays.copyOfRange(nums, 0, mid);
        left = sortArray(left);

        int[] right = Arrays.copyOfRange(nums, mid, nums.length);
        right = sortArray(right);

        return merge(left, right);
    }

    // merge two arrays
    private int[] merge (int[] left, int[] right) {
        int[] res = new int[left.length + right.length];
        int lIndex = 0, rIndex = 0;

        for (int i = 0; i < res.length; i++) {
            if (lIndex < left.length && rIndex < right.length) {
                if (left[lIndex] <= right[rIndex]) {
                    res[i] = left[lIndex++];
                } else {
                    res[i] = right[rIndex++];
                }
            } else if (lIndex >= left.length) {
                res[i] = right[rIndex++];
            } else {
                res[i] = left[lIndex++];
            }
        }

        return res;
    }
    ```
  
  + quick-sort
    ```js
    public int[] sortArray(int[] nums) {
        if (nums.length <= 1) return nums;
        qSort(nums, 0, nums.length - 1);
        return nums;
    }

    private void qSort(int[] nums, int s, int e) {
        int l = s, r = e;
        int temp = nums[l];
        while (l < r) {
            while (l < r && nums[r] >= temp) r--;
            if (l < r) nums[l++] = nums[r];
            while (l < r && nums[l] < temp) l++;
            if (l < r) nums[r--] = nums[l];
        }
        nums[l] = temp;
        if (s < l - 1) qSort(nums, s, l - 1);
        if (e > l + 1) qSort(nums, l + 1, e);
    }
    ```

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
  * set like an array but with no duplicates and in no fixed order
  * the element in a set are called member
  * set.size() get the size or cardinality of a set
  * set.isEmpty() if there is an empty set, return true
  * set.contains() check if this element in the set
  * set.containsAll() check the subsumes
  * set.equals() compare two sets. returen true if they are equal
  * set.clear() make set empty
  * set.add() add member into set
  * set.remove() remove the member in set
  * set.addAll(Set<E> that) add a set into another one
  * set.removeAll, set.retainAll()


## Map
#### properties
  * like map = {key1: value1, key2: value2, ...}
  * basic operations like previous ADTs
    + map.isEmpty(), map.clear()
    + map.size()
    + map.equals()
    + map.remove(key)
  * map.get(key) get the value of key
  * map.keySets() return a set including all keys of map
  * map1.putAll(map2) overlay the map1 with map2

#### classic problems
  * Using map to record some data to solve problems, like two sum
    ```js
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            if (map.containsKey(target - nums[i])) {
                return new int[]{map.get(target- nums[i]), i};
            }
            map.put(nums[i], i);
        }
        return new int[0];
    }
    ```


## Binary Search Tree
#### properties
  * left.val < root.val < right.val (ordered)
  * good for searching

#### classic problems
  * Validate Binary Search Tree
    ```js
    public long preVal = Long.MIN_VALUE;
    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;
        boolean isLeftValid = isValidBST(root.left);
        if (!isLeftValid) return false;
        if (root.val <= preVal) {
            return false;
        } else {
            preVal = root.val;
        }
        return isValidBST(root.right);
    }
    ```

## Hash
#### properties
  * Any type of data is mapped to a hash table by using a hashing algorithm to obtain a hash value.
  * **hash collison:** The mapping process generates hash collisions. There are two ways to handle collisions, either by placing subsequent elements directly below the collision point(the size of hashtable must greater than the number of elements) which is called open-bucket hashtable, or by creating a set at the collision point to place multiple elements that collide together which is called closed-bucket hashtable
  * **hash algorithm:** a great hash algorithm tend to make entries evenly among buckets
  * closed-bucket hash-table: each bucket should be occupied by at least two entries when a hash collision occurs
  * open-buckte hash-table: each bucket may be occupied by at most one entry. If there is a collision, put the new entry into another unoccupied bucket
  * search, delete is in O(1) time complexity

#### load factor
  * A reference for judging the suitability of hashing algorithms (usually between 0.5 and 0.75)
  if a load factor < 0.5, spaces are wasted
  if a laod factor > 0.75, some specific bucktes will contain much more entries than other buckets which is not beneficial to search
  * load factor is eauql to n (number of entries) / m (number of buckets)

#### exercises for selecting hash algorithm
  * judge hash function:
    + cosider m (number of buckets) = m
    + calculate load factor = n / m
    + value of load factor should between 0.5 and 0.75
  * select hash function:
    + n / load factor = m;
    + m should be a prime number since entries are more likely to be spread evenly.
    + hash function = xxxxx / modulo m; modulo m can control the hash value between 0 to m
