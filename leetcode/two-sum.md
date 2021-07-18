### [two-sum](https://leetcode.com/problems/two-sum)

## Approach 1 [Brute force]

Time : O(n-squared)
Space : O(1)

### explanation
- Simply go over each element for each each element in a nested for loop and check whether the sum equals the target 

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int i = 0; int j = 0;
        int[] ans = new int[2];
        for(i = 0; i < nums.length; i++) {
            for(j = 0; j < nums.length; j++) {
                if(target == (nums[i] + nums[j])) {
                    ans[0] = i;
                    ans[1] = j;
                    break;
                }
            }
        }
        return ans;
    }
}
``` 

```java
1. input: [2,7,11,15] & 9 | output: [1,0]
2. input: [3,2,4] & 6 | output: [2,1]
3. input: [3,3] & 6 | output: [1,0]
```

## Approach 2 [Using HashMap]

Time : O(n)
Space : O(n)

### explanation
- We start from the first element and keep storing it in a HashMap along with its index value
- Then, for every element henceforth, we look in this HashMap if it contains the key (target - item)
- If we fid it, then that is the solution

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> visitedMap = new HashMap<>();
        int answer[] = new int[2];
        
        for(int i=0; i<nums.length; i++) {
            if(visitedMap.containsKey(target - nums[i])) {
                answer[0] = visitedMap.get(target - nums[i]);
                answer[1] = i;
                break;
            }
            visitedMap.put(nums[i], i);
        }
        return answer;
    }
}
``` 

```java
same as above
```


## tags:
$tag1$
$tag2$
$tag3$