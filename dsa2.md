# Convert integer to the sum of two no zero integers

No-Zero integer is a positive integer that does not contain any 0 in its decimal representation.

Given an integer n, return a list of two integers [a, b] where:

a and b are No-Zero integers.
a + b = n
The test cases are generated so that there is at least one valid solution. If there are many valid solutions, you can return any of them.

 

Example 1:

Input: n = 2
Output: [1,1]
Explanation: Let a = 1 and b = 1.
Both a and b are no-zero integers, and a + b = 2 = n.
Example 2:

Input: n = 11
Output: [2,9]
Explanation: Let a = 2 and b = 9.
Both a and b are no-zero integers, and a + b = 11 = n.
Note that there are other valid answers as [8, 3] that can be accepted.
 

Constraints:

2 <= n <= 104





## Approach 
- Split a number n into two integers a + b = n, where neither a nor b contains the digit 0. Sounds simple? But it’s trickier than it looks
- The first thought is brute force: randomly trying pairs until you find one. But that’s messy and unclear. Instead, I loop through every possible a and check if both a and b = n - a are valid. Straightforward.
- The smart trick is writing a helper function isValid(). It checks if a number has digit 0 or not. With that, my main logic becomes super clean. For every a, just test isValid(a) and isValid(b).
- Why I like this method:
- - It’s brute force, but runs fast enough because range is small.
- - Easy to write and understand.
- - Debugging is simple, since isValid() can be tested separately.
- The lesson: Not every problem needs a fancy optimized approach. Sometimes looping + a helper function is the cleanest way. Simple code is easier to explain, maintain, and trust in real interviews.







```cpp
class Solution {
public:
    vector<int> getNoZeroIntegers(int n) {
        for (int a = 1; a < n; a++) {
            int b = n - a;
            if (isValid(a) && isValid(b)) {
                return {a, b};
            }
        }
        return {};
    }

private:
    bool isValid(int num) {
        while (num > 0) {
            if (num % 10 == 0) return false;
            num /= 10;
        }
        return true;
    }
};
```
