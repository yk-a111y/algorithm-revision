## Array

#### properties
  + array.length() => get the size of array
  + array[index] => access element using index
  + 

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

## Stack & Queue

#### basic operations

## Set

## Map

## Binary Tree

## Hash