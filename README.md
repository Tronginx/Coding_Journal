# 刷题日记

Learning algorithm is not as hard as many people may imagine. However, it takes time to show the consequence. Be patient, be respectful and be consistent. 

## Array 数组

5.8

占用连续的内存，查询O（1），插入删除O（N）

### 704 **binary search:**

第一遍看： 把nums分成两半，和target 进行比较，

if target 大于左边最小的 && 小于 left 中最大的就进入左边

else 进入右边

为什么pivot = (left + right) /2 是错的， 因为如果如果left + right 超过了integer的最大值，就会有问题

所以我们用 pivot = left  + (left-right)/2

难点：while loop 的条件是 left ≤ right

### 27.**Remove Element**

### 977 **Squares of a Sorted Array**

比较最左端 与最右端的绝对值

if left < right

square = nums[left]

left ++

else

square  = numsp[right]

rigth

1. **Minimum Size Subarray Sum**

### **59. Spiral Matrix II**

```jsx
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res = new int[n][n];
        int layer = n+1/2;
        int fill = 1;
        for(int i =0;i<layer;i++){
            for(int one=i;one<=n-i-2;one++){
                res[i][one] = fill++;
            }
            for(int two=i;two<=n-i-2;two++){
                res[two][n-i-1] = fill++;
            }            
            for(int three=n-i-1;three>i;three--){
                res[n-i-1][three] = fill++;
            }               
            for(int four=n-i-1;four>i;four--){
                res[four][i] = fill++;
            }    
            if (n % 2 == 1) {
            res[n/2][n/2] = fill;
        }
            
        }

        return res;
    }
}
```

### 35.**Search Insert Position**

## Linked List 链表

5.9

203. ### **Remove Linked List Elements**

```JAVA
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
    public ListNode removeElements(ListNode head, int val) {
        
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;
        
        ListNode prev = sentinel;
        ListNode curr = sentinel.next;
        
        while(curr != null){
            if(curr.val == val){
                prev.next = curr.next;            
            }
            else{
            prev = curr;

            }
            curr = curr.next;
        }
        
        return sentinel.next;

        

    }
}
```

- set sentinel/dummy node
- if curr.val == val, prev need to skip curr and connect to the next
- else prev move forward to curr
- Currently keep moving forward

707. ### **Design Linked List**

Will come back later

## LinkedList Revisit 

5.12

What is linked list?

Singly Linked List

- every node has two fields:
  - value 
  - pointer to next node.

Doubly Linked List

- has three fields:
  - value
  - pointer to previous node
  - pointer to next node

Constructor of Linked List:

```java
public class ListNode {
  int val;
  ListNode next;
  ListNode prev;
  ListNode(int x) { val = x; }
}
```

Delete a node

#### 203 Remove Linked List Elements

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
    public ListNode removeElements(ListNode head, int val) {
      
        if(head == null){
            return null;        
        }
        
        ListNode dummy = new ListNode(-1,head);
        ListNode prev = new ListNode();
        ListNode curr = new ListNode();
        
        prev = dummy;
        curr = head;
        
        while(curr != null){
            if(curr.val == val){
                prev.next = curr.next;
            }
            else{
                prev = prev.next;
            }
            curr = curr.next;
            
            
        }
        
        return dummy.next;

            
        

    }
}
```



#### 707.Design Linked List

- remember to check boundary every time!!!

- `index <size || index >= size` . We need to pay extra attention to index >= size, size the object is 0-indexed.

#### 206.Reverse Linked List

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
    public ListNode reverseList(ListNode head) {
        if(head == null){
            return null;
        }
        
        ListNode curr = new ListNode();
        ListNode prev = new ListNode();
        ListNode temp = new ListNode();
        
        prev = null;
        curr = head;
        temp = null;
        
        while(curr != null){
            temp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = temp;
            
            
        }
        return prev;
        
    }
}
```



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
    public ListNode reverseList(ListNode head) {
        
        return reverse(null,head);
        
    }
    
    public ListNode reverse(ListNode prev, ListNode curr){
        
        if(curr == null){
            return prev;
        }
        
        ListNode temp = null;
        temp = curr.next;
        curr.next = prev;

        
        return reverse(curr,temp);
    }
}
```

#### 24.Swap Nodes in Pairs

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
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null){
            return head;
        }
        
        ListNode first = new ListNode();
        ListNode second = new ListNode();
        
        first = head;
        second = head.next;
        
        first.next = swapPairs(second.next);
        second.next = first;
        
        return second;
    }
}
```

#### 19.Remove Nth Node From End of List

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if(head == null || head.next == null){
            return null;
        }
        
        int size = 0;
        ListNode curr = new ListNode();
        curr = head;
        while(curr != null){
            curr = curr.next;
            size ++;
        }
    
        
        int targetIndex = size -n;

        
        ListNode dummy = new ListNode();
        ListNode prev = new ListNode();

        dummy.next = head;
        prev = dummy;

        
        for(int i=0; i<targetIndex;i++){
            prev = prev.next;

            
        }
        prev.next = prev.next.next;
        
        return dummy.next;
        
    }
}
```

#### 160.tersection of Two Linked Lists

Brute Force

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null){
            return null;
        }
        
        ListNode currA = headA;
        ListNode currB = headB;
        
        while(currA != null){
            currB = headB;
            while(currB !=null){
                if(currA == currB){
                    return currA;
                }
                currB = currB.next;
            }
            currA = currA.next;
            
        }
        
        return null;
        
        
    }
}
```
Two pointers
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null){
            return null;
        }
        
        ListNode pointerA = headA;
        ListNode pointerB = headB;
        
        while(pointerA != pointerB){
            if(pointerA == null){
                pointerA = headB;
            }
            else{
                pointerA = pointerA.next;
            }
            
            if(pointerB == null){
                pointerB = headA;
            }
            else{
                pointerB = pointerB.next;
            }            
            
        }
        return pointerA;
        
    }
}
```

#### 142.Linked List Cycle II

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        
        while(fast != null && fast.next !=null){
            slow = slow.next;
            fast = fast.next.next;
            
            if(slow == fast){
                ListNode index1 = fast;
                ListNode index2 = head;
                
                while(index1 != index2){
                    index1 = index1.next;
                    index2 = index2.next;
                }
                return index1;
            }           
        }
        return null;      
    }
}
```

## Hash Table 哈希表

5.13

#### 242.Valid Anagram

Approach 1: sorting 

char[] str1 = s.toCharArray();

Arrays.sort(str1);

- undestand how to convert a string to char array
- understand Arrays.sort, usually takes O(nlogn)
- undestand Arrays.equals to compare arrays.

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length()){
            return false;
        }
        
        char[] sArray = s.toCharArray();
        char[] tArray = t.toCharArray();
        
        Arrays.sort(sArray);
        Arrays.sort(tArray);
        
        return Arrays.equals(sArray,tArray);
    }
}
```

Approach 2: counter 

- We set 26 position for 26 characters.
- for int i = 0; i<s.length();i++
  - counter[s.charAt[i] - 'a'] ++
  - counter[t.charAt[i] - 'a'] --
- for(int count : counter)
  - if(count != 0) return false;

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length()){
            return false;
        }
        int[] counter = new int[26];
        
        for(int i=0; i<s.length();i++){
           counter[s.charAt(i)-'a'] ++;
           counter[t.charAt(i)-'a'] --;
        }
        
        for(int count:counter){
            if(count != 0){
                return false;
            }
        }
                
        
        return true;
    }
}
```

#### 1002.Find Common Characters

5.14

暂时无法理解

#### 349.Intersection of Two Arrays

- build a hash set to store all the nums in nums1, since hash set only allows unique elements, we don't need to worry about duplicates
- build result hash set to store intersection of two arrays
- we use iterator of hash set to covert result hash set to result array which is required return type.

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        if(nums1 == null || nums2 == null){
            return new int[0];
        }
        
        HashSet<Integer> set1 = new HashSet<>();
        HashSet<Integer> resSet = new HashSet<>();
        
        for(int i : nums1){
            set1.add(i);
        }
        
        for(int i : nums2){
            if(set1.contains(i)){
                resSet.add(i);
            }
        }
        
        int[] res = new int[resSet.size()];
        int index = 0;
        for(int entry : resSet){
            res[index++] = entry;

        }
        
        return res;
        
        
    }
}
```

#### 202.Happy Number

- calculate the sum of squre of each digit
- while true
  - If happyNumber = 1 return true;
  - if happyNumber = prev return false;

```java
class Solution {
    public boolean isHappy(int n) {
        
        HashSet<Integer> set = new HashSet<>();
        while(true){
            int sum = calSum(n); 
            if(sum == 1){
                return true;
            }
            if(set.contains(sum)){
                return false;
            }
            else{
                set.add(sum);
            }
            n = sum;   
        }   
    }
    
    public int calSum(int n){
        int result = 0;
        while(n>0){
           int temp = n%10;
           result += temp*temp;
           n = n/10;
        }     
        return result;       
    }    
}
```

#### 1.Two Sum

- if nums == null; return null
- for i=0;i<nums.length;i++
  - calculate diff = target - nums[i]
  - look up diff in the Map to decide if the required partner exsited
  - if existed: return i and map.get(diff)
  - map.put(nums[i],i)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[2];
        if(nums == null){
            return res;
        }
        
        Map<Integer,Integer> map = new HashMap<>();
        for(int i=0;i<nums.length;i++){
            int dif = target - nums[i];
            if(map.containsKey(dif)){
                res[0] = i;
                res[1] = map.get(dif);
            }
            map.put(nums[i],i);
        }
        return res;
    }
}
```

5.16

#### 454.4Sum II

```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        int cnt =0;
        Map<Integer,Integer> map = new HashMap<>();
        for(int a:nums1){
            for(int b:nums2){
                map.put(a + b, map.getOrDefault(a + b, 0) + 1);
            }
        }        
         for(int c : nums3){
            for(int d : nums4){
                cnt += map.getOrDefault(-(c+d),0);
            }
        }       
        return cnt;
    }     
  }

```

#### 383.Ransom Note

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int[] counter = new int[26];      
        for(int i=0;i<magazine.length();i++){
            counter[magazine.charAt(i)-'a']++;
        }
        for(int i=0; i<ransomNote.length();i++){
            char x = ransomNote.charAt(i);
            counter[x-'a']--;
            
        }
        for(int x:counter){
            if(x<0){
                return false;
            }
        }
        return true;
    }
}
```

#### 15.3Sum

## String

5.18

#### 344.Reverse String

5.21

```java
class Solution {
    public void reverseString(char[] s) {    
        int len = s.length;
        if(len ==0 || len ==1){
            return;
        }
            for(int i=0; i<len/2;i++){
                char temp = s[i];
                s[i] = s[len-i-1];
                s[len-i-1] = temp;
            }
    }
}
```

#### 541.Reverse String II

暂时不提

#### 剑指offer 05 Replace Space with %20

```java
class Solution {
    public String replaceSpace(String s) {
        if (s == null) {
            return null;
        }
        StringBuilder sb = new StringBuilder();
        for(int i =0; i<s.length();i++){
            if(s.charAt(i) == ' '){
                sb.append("%20");
            }
            else{
                sb.append(s.charAt(i));
            }
        }
        return sb.toString();
    }
}
```

