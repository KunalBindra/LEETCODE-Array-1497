# LEETCODE-Array-1497
Let's walk through a dry run of the provided solution to the problem.

### Problem Understanding:
Given an integer array `arr` and an integer `k`, we need to determine if it is possible to rearrange the array into pairs such that the sum of every pair is divisible by `k`.

### Code Explanation:
```java
public boolean canArrange(int[] arr, int k) {
    int[] count = new int[k];  // Array to store the count of remainders when divided by k.

    // Step 1: Calculate the remainder of each element when divided by k and update the count array.
    for (int a : arr) {
        a %= k;  // Find the remainder when a is divided by k.
        // Handle negative remainders by adjusting them to a positive equivalent.
        ++count[a < 0 ? a + k : a];  // Increment the count of the remainder.
    }

    // Step 2: Check if the count of elements with remainder 0 is even.
    if (count[0] % 2 != 0)
        return false;  // If there are odd numbers of remainder 0, pairing isn't possible.

    // Step 3: Check if counts of i and k-i are equal for 1 <= i <= k/2.
    for (int i = 1; i <= k / 2; i++) {
        if (count[i] != count[k - i])
            return false;  // If they are not equal, pairing isn't possible.
    }

    return true;  // All conditions satisfied, return true.
}
```

### Dry Run:

#### Test Case:
Input: `arr = [2, -2, 3, -3, 4, -4]`, `k = 5`

1. **Step 1: Process each element of `arr`**:
   - For `2`:  
     - `2 % 5 = 2` → `count[2]++` → `count = [0, 0, 1, 0, 0]`
   - For `-2`:  
     - `-2 % 5 = -2`, adjust → `-2 + 5 = 3` → `count[3]++` → `count = [0, 0, 1, 1, 0]`
   - For `3`:  
     - `3 % 5 = 3` → `count[3]++` → `count = [0, 0, 1, 2, 0]`
   - For `-3`:  
     - `-3 % 5 = -3`, adjust → `-3 + 5 = 2` → `count[2]++` → `count = [0, 0, 2, 2, 0]`
   - For `4`:  
     - `4 % 5 = 4` → `count[4]++` → `count = [0, 0, 2, 2, 1]`
   - For `-4`:  
     - `-4 % 5 = -4`, adjust → `-4 + 5 = 1` → `count[1]++` → `count = [0, 1, 2, 2, 1]`

2. **Step 2: Check if count of elements with remainder 0 is even**:
   - `count[0] = 0`, which is even, so we continue.

3. **Step 3: Check if count[i] matches count[k - i]**:
   - For `i = 1`, `count[1] = 1` and `count[4] = 1`. They match.
   - For `i = 2`, `count[2] = 2` and `count[3] = 2`. They match.

Since all conditions are satisfied, the function returns `**true**`.

### Conclusion:
The input `[2, -2, 3, -3, 4, -4]` with `k = 5` can be rearranged into pairs such that the sum of each pair is divisible by 5. Hence, the output is `true`.
