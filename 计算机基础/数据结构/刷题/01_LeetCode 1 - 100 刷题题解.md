# LeetCode 1 - 100 刷题题解

## [1. 两数之和](https://leetcode.cn/problems/two-sum/)

```java
// 1. 开始想的是，建立 哈希表，来进行；两遍 for 循环即可；
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++) {
            map.put(nums[i], i);
        }

        for(int i = 0; i < nums.length; i++) {
            if(map.containsKey(target - nums[i]) && i != map.get(target - nums[i])) {
                return new int[]{i, map.get(target- nums[i])};
            }
        }
        
        return null;
    }
}

// 2. 但是这样的话，时间上并非是最省时间的；因为可以在遍历的过程之中解决；
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>(nums.length);

        for(int i = 0; i < nums.length; i++) {
            if(map.containsKey(target - nums[i])) {
                return new int[]{i, map.get(target-nums[i])};
            }
            map.put(nums[i], i);
        }
        
        return null;
    }
}
```

## [2. 两数相加](https://leetcode.cn/problems/add-two-numbers/)

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

// 基本模拟思路
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int carry = 0, tmp;
        ListNode header = new ListNode();
        ListNode p = header;
        while(l1 != null && l2 != null) {
            tmp = l1.val + l2.val + carry;
            
            ListNode node = new ListNode(tmp%10);
            p.next = node;
            p = node;
            carry = tmp / 10;
            l1 = l1.next;
            l2 = l2.next;
        }
        while(l1 != null) {
            tmp = l1.val + carry;
            ListNode node = new ListNode(tmp%10);
            p.next = node;
            p = node;
            carry = tmp / 10;
            l1 = l1.next;
        }
        while(l2 != null) {
            tmp = l2.val + carry;
            ListNode node = new ListNode(tmp%10);
            p.next = node;
            p = node;
            carry = tmp / 10;
            l2 = l2.next;
        }
        if(carry != 0) {
            ListNode node = new ListNode(carry);
            p.next = node;
        }

        return header.next;
    }
}


// 优化好看点代码，但实际上判断比上面的多；
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode res = new ListNode();
        ListNode p = res;
        int carry = 0;
        while(l1 != null || l2 != null) {
            carry = (l1 ==  null ? 0 : l1.val) + (l2 == null ? 0 : l2.val )  + carry;
            ListNode tmp = new ListNode(carry%10);
            carry = carry / 10;
            p.next = tmp;

            p = p.next;
            if(l1 != null) l1 = l1.next;
            if(l2 != null) l2 = l2.next;
        }

        if(carry != 0) {
            ListNode tmp = new ListNode(carry);
            p.next = tmp;
        }

        return res.next;
    }
}

```

## [3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

```java
// 简单滑动窗口，考虑每个字符开始的时候，不包含重复字符的最长子串；典型双指针问题；
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int l = 0 , r = 0, len = s.length(), res = 0;
        int cnt[] = new int [128];
        while(l <=r && r < len) {
            if(cnt[s.charAt(r)] == 0) {
                cnt[s.charAt(r)]++;
                res = Math.max(res, r - l + 1);
                r++;
            }
            else {
                res = Math.max(res, r - l);
                cnt[s.charAt(l)]--;
                l++;
            }
        }
        return res;
    }
}
```

