### [happy-number](https://leetcode.com/problems/happy-number/)

## Approach 1 [Using HashSet]

Time : O(length of the chain)
Space : O(length of the chain)

where, length of the chain = number of non repeating sum values that occur

### explanation
- For numbers for which the sums do not end in `1`, the sum values start repeating at some point
- So, if we keep adding the sum values to a HashSet and check if the next sum value already exists in that set,
  - if we reach 1, then we are good, 
  - else, we will reach a sum that would already exist in the set, and that would make the original number not happy.

```java
class Solution {
    public boolean isHappy(int n) {
        Set sumSet = new HashSet<>();
        
        while(true) {
            int s = getDigitSumSquare(n);
            if(s == 1) return true;
            if(sumSet.contains(s)) return false;
            sumSet.add(s);
            n = s;
        }
    }
    
    private int getDigitSumSquare(int n){
        int sum = 0;
        while(n != 0) {
            sum += (n%10)*(n%10);
            n = n/10;
        }
        return sum;
    }   
}
``` 

```java
input1: 19 | output1: true
input2: 4 | output1: false
```

## Approach 1' [Using Hashset, with optimizations]

### explanation

- we can precalculate some cases that could lead to verry long chains, and add special checks for them intead of waiting till appearance of either 1 or repeated sum to stop the loop.

## Approach 2 [Using Floyd Cycle Detection]

Time : O(length of the chain)
Space : O(1)

where, length of the chain = number of non repeating sum values that occur

### explanation
- instead of maintaining a HasSet as in above approach, we will use the Floyd Cycle Detction approach for figuring out if sums are repeating or not.
- Whenever going on a cycle, two runners of different speeds will eventually catch up
- In both cases for the happy number, there are cycles:
  - For happy Number - it is eventually a single state cycle of sums all at state sum=1
  - For non-happy Number - all sums form a cycle from the starting
- So, we simply need to keep getting the sums for two different speeds, which will eventually collide
- At collision, we check whether collided sums (which would be equal for both speeds) = 1 or not
  - If equal to 1, then original number is a happy number
  - Else, not a happy number

```java
class Solution {
    public boolean isHappy(int n) {
        int slow = n;
        int fast = n;
        
        while(true) {
            slow = getDigitSumSquare(slow);
            fast = getDigitSumSquare(getDigitSumSquare(fast));
            
            if (fast == 1) return true;
            if(slow == fast) return false;
        }
    }
    
    private int getDigitSumSquare(int n){
        int sum = 0;
        while(n != 0) {
            sum += (n%10)*(n%10);
            n = n/10;
        }
        return sum;
    }   
}
``` 

```java
input1: 19 | output1: true
input2: 4 | output1: false
```

## tags:
$hashset$
$cycledetection$