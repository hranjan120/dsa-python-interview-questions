# DSA Solutions in Python — Arrays, Strings & Recursion

A complete reference of commonly asked DSA questions with Python solutions and examples.

---

## Table of Contents

1. [Arrays - Easy](#arrays---easy)
2. [Arrays - Medium](#arrays---medium)
3. [Strings - Easy](#strings---easy)
4. [Strings - Medium](#strings---medium)
5. [Recursion / Backtracking - Easy](#recursion--backtracking---easy)
6. [Recursion / Backtracking - Medium](#recursion--backtracking---medium)

---

# Arrays - Easy

## 1. Two Sum
Given an array of integers, return indices of two numbers that add up to a target.

```python
def two_sum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        diff = target - num
        if diff in seen:
            return [seen[diff], i]
        seen[num] = i
    return []

# Example
print(two_sum([2, 7, 11, 15], 9))  # Output: [0, 1]
```

## 2. Best Time to Buy and Sell Stock
Find max profit from a single buy-sell transaction.

```python
def max_profit(prices):
    min_price = float('inf')
    profit = 0
    for price in prices:
        min_price = min(min_price, price)
        profit = max(profit, price - min_price)
    return profit

# Example
print(max_profit([7, 1, 5, 3, 6, 4]))  # Output: 5
```

## 3. Maximum Subarray (Kadane's Algorithm)
Find contiguous subarray with the largest sum.

```python
def max_subarray(nums):
    max_sum = current = nums[0]
    for num in nums[1:]:
        current = max(num, current + num)
        max_sum = max(max_sum, current)
    return max_sum

# Example
print(max_subarray([-2, 1, -3, 4, -1, 2, 1, -5, 4]))  # Output: 6
```

## 4. Pascal's Triangle
Generate the first numRows of Pascal's Triangle.

```python
def generate_pascal(num_rows):
    triangle = []
    for i in range(num_rows):
        row = [1] * (i + 1)
        for j in range(1, i):
            row[j] = triangle[i-1][j-1] + triangle[i-1][j]
        triangle.append(row)
    return triangle

# Example
print(generate_pascal(5))
# Output: [[1], [1,1], [1,2,1], [1,3,3,1], [1,4,6,4,1]]
```

## 5. Majority Element
Find element that appears more than n/2 times (Boyer-Moore Voting).

```python
def majority_element(nums):
    count = 0
    candidate = None
    for num in nums:
        if count == 0:
            candidate = num
        count += 1 if num == candidate else -1
    return candidate

# Example
print(majority_element([2, 2, 1, 1, 1, 2, 2]))  # Output: 2
```

## 6. Move Zeroes
Move all zeros to end while maintaining order of non-zero elements.

```python
def move_zeroes(nums):
    pos = 0
    for i in range(len(nums)):
        if nums[i] != 0:
            nums[pos], nums[i] = nums[i], nums[pos]
            pos += 1
    return nums

# Example
print(move_zeroes([0, 1, 0, 3, 12]))  # Output: [1, 3, 12, 0, 0]
```

## 7. Remove Duplicates from Sorted Array
Remove duplicates in-place and return new length.

```python
def remove_duplicates(nums):
    if not nums:
        return 0
    k = 1
    for i in range(1, len(nums)):
        if nums[i] != nums[i-1]:
            nums[k] = nums[i]
            k += 1
    return k

# Example
nums = [1, 1, 2, 2, 3]
print(remove_duplicates(nums))  # Output: 3 (array becomes [1,2,3,...])
```

## 8. Merge Sorted Array
Merge two sorted arrays into the first one (in-place).

```python
def merge(nums1, m, nums2, n):
    i, j, k = m - 1, n - 1, m + n - 1
    while i >= 0 and j >= 0:
        if nums1[i] > nums2[j]:
            nums1[k] = nums1[i]
            i -= 1
        else:
            nums1[k] = nums2[j]
            j -= 1
        k -= 1
    while j >= 0:
        nums1[k] = nums2[j]
        j -= 1
        k -= 1
    return nums1

# Example
print(merge([1, 2, 3, 0, 0, 0], 3, [2, 5, 6], 3))
# Output: [1, 2, 2, 3, 5, 6]
```

## 9. Contains Duplicate
Check if array contains any duplicates.

```python
def contains_duplicate(nums):
    return len(nums) != len(set(nums))

# Example
print(contains_duplicate([1, 2, 3, 1]))  # Output: True
```

## 10. Find Missing Number
Find missing number in array containing 0 to n.

```python
def missing_number(nums):
    n = len(nums)
    return n * (n + 1) // 2 - sum(nums)

# Example
print(missing_number([3, 0, 1]))  # Output: 2
```

## 11. Single Number
Every element appears twice except one — find it (XOR trick).

```python
def single_number(nums):
    result = 0
    for num in nums:
        result ^= num
    return result

# Example
print(single_number([4, 1, 2, 1, 2]))  # Output: 4
```

## 12. Rotate Array
Rotate array to the right by k steps.

```python
def rotate(nums, k):
    k %= len(nums)
    nums[:] = nums[-k:] + nums[:-k]
    return nums

# Example
print(rotate([1, 2, 3, 4, 5, 6, 7], 3))  # Output: [5, 6, 7, 1, 2, 3, 4]
```

---

# Arrays - Medium

## 1. Set Matrix Zeroes
If an element is 0, set its entire row and column to 0.

```python
def set_zeroes(matrix):
    rows, cols = set(), set()
    for i in range(len(matrix)):
        for j in range(len(matrix[0])):
            if matrix[i][j] == 0:
                rows.add(i)
                cols.add(j)
    for i in range(len(matrix)):
        for j in range(len(matrix[0])):
            if i in rows or j in cols:
                matrix[i][j] = 0
    return matrix

# Example
print(set_zeroes([[1,1,1],[1,0,1],[1,1,1]]))
# Output: [[1,0,1],[0,0,0],[1,0,1]]
```

## 2. Next Permutation
Find next lexicographically greater permutation.

```python
def next_permutation(nums):
    i = len(nums) - 2
    while i >= 0 and nums[i] >= nums[i + 1]:
        i -= 1
    if i >= 0:
        j = len(nums) - 1
        while nums[j] <= nums[i]:
            j -= 1
        nums[i], nums[j] = nums[j], nums[i]
    nums[i+1:] = reversed(nums[i+1:])
    return nums

# Example
print(next_permutation([1, 2, 3]))  # Output: [1, 3, 2]
```

## 3. Sort Colors (0s, 1s, 2s) — Dutch National Flag
Sort array containing only 0, 1, and 2 in single pass.

```python
def sort_colors(nums):
    low, mid, high = 0, 0, len(nums) - 1
    while mid <= high:
        if nums[mid] == 0:
            nums[low], nums[mid] = nums[mid], nums[low]
            low += 1
            mid += 1
        elif nums[mid] == 1:
            mid += 1
        else:
            nums[mid], nums[high] = nums[high], nums[mid]
            high -= 1
    return nums

# Example
print(sort_colors([2, 0, 2, 1, 1, 0]))  # Output: [0, 0, 1, 1, 2, 2]
```

## 4. Rotate Matrix by 90 Degrees
Rotate n x n matrix clockwise by 90 degrees.

```python
def rotate_matrix(matrix):
    n = len(matrix)
    # Transpose
    for i in range(n):
        for j in range(i, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    # Reverse each row
    for row in matrix:
        row.reverse()
    return matrix

# Example
print(rotate_matrix([[1,2,3],[4,5,6],[7,8,9]]))
# Output: [[7,4,1],[8,5,2],[9,6,3]]
```

## 5. Merge Intervals
Merge all overlapping intervals.

```python
def merge_intervals(intervals):
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]
    for start, end in intervals[1:]:
        if start <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], end)
        else:
            merged.append([start, end])
    return merged

# Example
print(merge_intervals([[1,3],[2,6],[8,10],[15,18]]))
# Output: [[1,6],[8,10],[15,18]]
```

## 6. Merge Two Sorted Arrays Without Extra Space
Merge in-place using gap method.

```python
def merge_no_extra_space(arr1, arr2):
    n, m = len(arr1), len(arr2)
    i, j = n - 1, 0
    while i >= 0 and j < m:
        if arr1[i] > arr2[j]:
            arr1[i], arr2[j] = arr2[j], arr1[i]
            i -= 1
            j += 1
        else:
            break
    arr1.sort()
    arr2.sort()
    return arr1, arr2

# Example
print(merge_no_extra_space([1, 4, 7, 8, 10], [2, 3, 9]))
# Output: ([1, 2, 3, 4, 7], [8, 9, 10])
```

## 7. Find the Duplicate Number
Find the duplicate in array of n+1 integers (Floyd's cycle).

```python
def find_duplicate(nums):
    slow = fast = nums[0]
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast:
            break
    slow = nums[0]
    while slow != fast:
        slow = nums[slow]
        fast = nums[fast]
    return slow

# Example
print(find_duplicate([1, 3, 4, 2, 2]))  # Output: 2
```

## 8. 3 Sum
Find all unique triplets that sum to zero.

```python
def three_sum(nums):
    nums.sort()
    result = []
    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i-1]:
            continue
        left, right = i + 1, len(nums) - 1
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            if total == 0:
                result.append([nums[i], nums[left], nums[right]])
                while left < right and nums[left] == nums[left+1]:
                    left += 1
                while left < right and nums[right] == nums[right-1]:
                    right -= 1
                left += 1
                right -= 1
            elif total < 0:
                left += 1
            else:
                right -= 1
    return result

# Example
print(three_sum([-1, 0, 1, 2, -1, -4]))
# Output: [[-1, -1, 2], [-1, 0, 1]]
```

## 9. 4 Sum
Find unique quadruplets that sum to target.

```python
def four_sum(nums, target):
    nums.sort()
    result = []
    n = len(nums)
    for i in range(n - 3):
        if i > 0 and nums[i] == nums[i-1]:
            continue
        for j in range(i + 1, n - 2):
            if j > i + 1 and nums[j] == nums[j-1]:
                continue
            left, right = j + 1, n - 1
            while left < right:
                total = nums[i] + nums[j] + nums[left] + nums[right]
                if total == target:
                    result.append([nums[i], nums[j], nums[left], nums[right]])
                    while left < right and nums[left] == nums[left+1]:
                        left += 1
                    while left < right and nums[right] == nums[right-1]:
                        right -= 1
                    left += 1
                    right -= 1
                elif total < target:
                    left += 1
                else:
                    right -= 1
    return result

# Example
print(four_sum([1, 0, -1, 0, -2, 2], 0))
# Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

## 10. Longest Consecutive Sequence
Find the length of the longest consecutive elements sequence.

```python
def longest_consecutive(nums):
    num_set = set(nums)
    longest = 0
    for num in num_set:
        if num - 1 not in num_set:
            current = num
            length = 1
            while current + 1 in num_set:
                current += 1
                length += 1
            longest = max(longest, length)
    return longest

# Example
print(longest_consecutive([100, 4, 200, 1, 3, 2]))  # Output: 4
```

## 11. Largest Subarray with K Sum
Find length of longest subarray with sum equal to k.

```python
def longest_subarray_sum_k(nums, k):
    prefix_sum = 0
    sum_map = {}
    max_len = 0
    for i, num in enumerate(nums):
        prefix_sum += num
        if prefix_sum == k:
            max_len = i + 1
        if prefix_sum - k in sum_map:
            max_len = max(max_len, i - sum_map[prefix_sum - k])
        if prefix_sum not in sum_map:
            sum_map[prefix_sum] = i
    return max_len

# Example
print(longest_subarray_sum_k([10, 5, 2, 7, 1, 9], 15))  # Output: 4
```

## 12. Product of Array Except Self
Return array where each element is product of all others (no division).

```python
def product_except_self(nums):
    n = len(nums)
    result = [1] * n
    left = 1
    for i in range(n):
        result[i] = left
        left *= nums[i]
    right = 1
    for i in range(n - 1, -1, -1):
        result[i] *= right
        right *= nums[i]
    return result

# Example
print(product_except_self([1, 2, 3, 4]))  # Output: [24, 12, 8, 6]
```

## 13. Search in 2D Matrix
Search target in row & column sorted matrix.

```python
def search_matrix(matrix, target):
    if not matrix:
        return False
    rows, cols = len(matrix), len(matrix[0])
    left, right = 0, rows * cols - 1
    while left <= right:
        mid = (left + right) // 2
        val = matrix[mid // cols][mid % cols]
        if val == target:
            return True
        elif val < target:
            left = mid + 1
        else:
            right = mid - 1
    return False

# Example
print(search_matrix([[1,3,5,7],[10,11,16,20],[23,30,34,60]], 3))  # Output: True
```

## 14. Spiral Matrix
Return all elements of matrix in spiral order.

```python
def spiral_order(matrix):
    result = []
    while matrix:
        result += matrix.pop(0)
        if matrix and matrix[0]:
            for row in matrix:
                result.append(row.pop())
        if matrix:
            result += matrix.pop()[::-1]
        if matrix and matrix[0]:
            for row in matrix[::-1]:
                result.append(row.pop(0))
    return result

# Example
print(spiral_order([[1,2,3],[4,5,6],[7,8,9]]))
# Output: [1, 2, 3, 6, 9, 8, 7, 4, 5]
```

## 15. Subarray Sum Equals K
Count number of subarrays with sum equal to k.

```python
def subarray_sum(nums, k):
    count = 0
    prefix_sum = 0
    sum_map = {0: 1}
    for num in nums:
        prefix_sum += num
        if prefix_sum - k in sum_map:
            count += sum_map[prefix_sum - k]
        sum_map[prefix_sum] = sum_map.get(prefix_sum, 0) + 1
    return count

# Example
print(subarray_sum([1, 1, 1], 2))  # Output: 2
```

## 16. Container With Most Water
Find two lines that form container holding maximum water.

```python
def max_area(height):
    left, right = 0, len(height) - 1
    max_water = 0
    while left < right:
        area = min(height[left], height[right]) * (right - left)
        max_water = max(max_water, area)
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
    return max_water

# Example
print(max_area([1, 8, 6, 2, 5, 4, 8, 3, 7]))  # Output: 49
```

## 17. Grid Unique Paths
Count unique paths from top-left to bottom-right (only right/down moves).

```python
def unique_paths(m, n):
    dp = [[1] * n for _ in range(m)]
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
    return dp[m-1][n-1]

# Example
print(unique_paths(3, 7))  # Output: 28
```

## 18. Pow(x, n)
Compute x raised to power n efficiently.

```python
def my_pow(x, n):
    if n < 0:
        x = 1 / x
        n = -n
    result = 1
    while n > 0:
        if n % 2 == 1:
            result *= x
        x *= x
        n //= 2
    return result

# Example
print(my_pow(2.0, 10))  # Output: 1024.0
```

## 19. Majority Element II
Find all elements appearing more than n/3 times.

```python
def majority_element_ii(nums):
    if not nums:
        return []
    c1, c2, count1, count2 = 0, 1, 0, 0
    for num in nums:
        if num == c1:
            count1 += 1
        elif num == c2:
            count2 += 1
        elif count1 == 0:
            c1, count1 = num, 1
        elif count2 == 0:
            c2, count2 = num, 1
        else:
            count1 -= 1
            count2 -= 1
    return [c for c in {c1, c2} if nums.count(c) > len(nums) // 3]

# Example
print(majority_element_ii([3, 2, 3]))  # Output: [3]
```

## 20. Next Greater Element
For each element, find next greater element on its right.

```python
def next_greater_element(nums):
    result = [-1] * len(nums)
    stack = []
    for i in range(len(nums)):
        while stack and nums[stack[-1]] < nums[i]:
            result[stack.pop()] = nums[i]
        stack.append(i)
    return result

# Example
print(next_greater_element([4, 5, 2, 25]))  # Output: [5, 25, 25, -1]
```

---

# Strings - Easy

## 1. Valid Anagram
Check if two strings are anagrams.

```python
def is_anagram(s, t):
    return sorted(s) == sorted(t)

# Example
print(is_anagram("anagram", "nagaram"))  # Output: True
```

## 2. Longest Common Prefix
Find longest common prefix of array of strings.

```python
def longest_common_prefix(strs):
    if not strs:
        return ""
    prefix = strs[0]
    for s in strs[1:]:
        while not s.startswith(prefix):
            prefix = prefix[:-1]
            if not prefix:
                return ""
    return prefix

# Example
print(longest_common_prefix(["flower", "flow", "flight"]))  # Output: "fl"
```

## 3. Roman to Integer
Convert Roman numeral string to integer.

```python
def roman_to_int(s):
    values = {'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
    total = 0
    prev = 0
    for ch in reversed(s):
        curr = values[ch]
        if curr < prev:
            total -= curr
        else:
            total += curr
        prev = curr
    return total

# Example
print(roman_to_int("MCMXCIV"))  # Output: 1994
```

## 4. Valid Palindrome
Check if string is palindrome (alphanumeric only, case-insensitive).

```python
def is_palindrome(s):
    s = ''.join(c.lower() for c in s if c.isalnum())
    return s == s[::-1]

# Example
print(is_palindrome("A man, a plan, a canal: Panama"))  # Output: True
```

## 5. Reverse String
Reverse string in-place.

```python
def reverse_string(s):
    left, right = 0, len(s) - 1
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
    return s

# Example
print(reverse_string(['h','e','l','l','o']))  # Output: ['o','l','l','e','h']
```

## 6. Reverse Words in a String
Reverse the order of words.

```python
def reverse_words(s):
    return ' '.join(s.split()[::-1])

# Example
print(reverse_words("the sky is blue"))  # Output: "blue is sky the"
```

## 7. Implement strStr()
Find first occurrence of needle in haystack.

```python
def str_str(haystack, needle):
    if not needle:
        return 0
    for i in range(len(haystack) - len(needle) + 1):
        if haystack[i:i+len(needle)] == needle:
            return i
    return -1

# Example
print(str_str("hello", "ll"))  # Output: 2
```

## 8. Length of Last Word
Return length of the last word in string.

```python
def length_of_last_word(s):
    return len(s.strip().split(' ')[-1])

# Example
print(length_of_last_word("Hello World"))  # Output: 5
```

## 9. First Unique Character in a String
Return index of first non-repeating character.

```python
def first_uniq_char(s):
    from collections import Counter
    count = Counter(s)
    for i, ch in enumerate(s):
        if count[ch] == 1:
            return i
    return -1

# Example
print(first_uniq_char("leetcode"))  # Output: 0
```

## 10. Detect Capital
Check if usage of capitals in word is correct.

```python
def detect_capital(word):
    return word.isupper() or word.islower() or word.istitle()

# Example
print(detect_capital("USA"))    # Output: True
print(detect_capital("FlaG"))   # Output: False
```

---

# Strings - Medium

## 1. Longest Palindromic Substring
Find longest palindromic substring.

```python
def longest_palindrome(s):
    def expand(l, r):
        while l >= 0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        return s[l+1:r]
    
    result = ""
    for i in range(len(s)):
        odd = expand(i, i)
        even = expand(i, i+1)
        result = max(result, odd, even, key=len)
    return result

# Example
print(longest_palindrome("babad"))  # Output: "bab" or "aba"
```

## 2. Longest Substring Without Repeating Characters
Find length of longest substring without repeating characters.

```python
def length_of_longest_substring(s):
    seen = {}
    left = 0
    max_len = 0
    for right, ch in enumerate(s):
        if ch in seen and seen[ch] >= left:
            left = seen[ch] + 1
        seen[ch] = right
        max_len = max(max_len, right - left + 1)
    return max_len

# Example
print(length_of_longest_substring("abcabcbb"))  # Output: 3
```

## 3. String to Integer (ATOI)
Convert string to integer.

```python
def my_atoi(s):
    s = s.lstrip()
    if not s:
        return 0
    sign = 1
    i = 0
    if s[0] in ('+', '-'):
        sign = -1 if s[0] == '-' else 1
        i += 1
    result = 0
    while i < len(s) and s[i].isdigit():
        result = result * 10 + int(s[i])
        i += 1
    result *= sign
    return max(-2**31, min(2**31 - 1, result))

# Example
print(my_atoi("   -42"))  # Output: -42
```

## 4. Compare Version Numbers
Compare two version strings.

```python
def compare_version(v1, v2):
    p1 = list(map(int, v1.split('.')))
    p2 = list(map(int, v2.split('.')))
    for i in range(max(len(p1), len(p2))):
        a = p1[i] if i < len(p1) else 0
        b = p2[i] if i < len(p2) else 0
        if a != b:
            return 1 if a > b else -1
    return 0

# Example
print(compare_version("1.01", "1.001"))  # Output: 0
```

## 5. Group Anagrams
Group strings that are anagrams of each other.

```python
def group_anagrams(strs):
    from collections import defaultdict
    groups = defaultdict(list)
    for s in strs:
        groups[''.join(sorted(s))].append(s)
    return list(groups.values())

# Example
print(group_anagrams(["eat","tea","tan","ate","nat","bat"]))
# Output: [['eat','tea','ate'],['tan','nat'],['bat']]
```

## 6. Longest Repeating Character Replacement
Longest substring with same letter after k replacements.

```python
def character_replacement(s, k):
    count = {}
    left = 0
    max_count = 0
    result = 0
    for right in range(len(s)):
        count[s[right]] = count.get(s[right], 0) + 1
        max_count = max(max_count, count[s[right]])
        if right - left + 1 - max_count > k:
            count[s[left]] -= 1
            left += 1
        result = max(result, right - left + 1)
    return result

# Example
print(character_replacement("ABAB", 2))  # Output: 4
```

## 7. Minimum Window Substring
Find minimum window in s that contains all characters of t.

```python
def min_window(s, t):
    from collections import Counter
    if not t or not s:
        return ""
    need = Counter(t)
    have = {}
    have_count, need_count = 0, len(need)
    result = [-1, -1]
    result_len = float('inf')
    left = 0
    for right in range(len(s)):
        ch = s[right]
        have[ch] = have.get(ch, 0) + 1
        if ch in need and have[ch] == need[ch]:
            have_count += 1
        while have_count == need_count:
            if right - left + 1 < result_len:
                result = [left, right]
                result_len = right - left + 1
            have[s[left]] -= 1
            if s[left] in need and have[s[left]] < need[s[left]]:
                have_count -= 1
            left += 1
    l, r = result
    return s[l:r+1] if result_len != float('inf') else ""

# Example
print(min_window("ADOBECODEBANC", "ABC"))  # Output: "BANC"
```

## 8. Check Inclusion (Permutation in String)
Check if s2 contains a permutation of s1.

```python
def check_inclusion(s1, s2):
    from collections import Counter
    if len(s1) > len(s2):
        return False
    s1_count = Counter(s1)
    window = Counter(s2[:len(s1)])
    if window == s1_count:
        return True
    for i in range(len(s1), len(s2)):
        window[s2[i]] += 1
        window[s2[i - len(s1)]] -= 1
        if window[s2[i - len(s1)]] == 0:
            del window[s2[i - len(s1)]]
        if window == s1_count:
            return True
    return False

# Example
print(check_inclusion("ab", "eidbaooo"))  # Output: True
```

## 9. Palindrome Partitioning
Partition string so every substring is a palindrome (return all).

```python
def palindrome_partition(s):
    result = []
    def is_pal(sub):
        return sub == sub[::-1]
    def backtrack(start, path):
        if start == len(s):
            result.append(path[:])
            return
        for end in range(start + 1, len(s) + 1):
            if is_pal(s[start:end]):
                path.append(s[start:end])
                backtrack(end, path)
                path.pop()
    backtrack(0, [])
    return result

# Example
print(palindrome_partition("aab"))
# Output: [['a','a','b'], ['aa','b']]
```

## 10. Encode and Decode Strings
Encode list of strings to single string and decode back.

```python
def encode(strs):
    return ''.join(f"{len(s)}#{s}" for s in strs)

def decode(s):
    result = []
    i = 0
    while i < len(s):
        j = s.index('#', i)
        length = int(s[i:j])
        result.append(s[j+1:j+1+length])
        i = j + 1 + length
    return result

# Example
encoded = encode(["hello", "world"])
print(encoded)         # Output: "5#hello5#world"
print(decode(encoded)) # Output: ['hello', 'world']
```

## 11. Count and Say
Generate the nth term of count-and-say sequence.

```python
def count_and_say(n):
    s = "1"
    for _ in range(n - 1):
        result = ""
        i = 0
        while i < len(s):
            count = 1
            while i + 1 < len(s) and s[i] == s[i+1]:
                i += 1
                count += 1
            result += str(count) + s[i]
            i += 1
        s = result
    return s

# Example
print(count_and_say(4))  # Output: "1211"
```

## 12. Zigzag Conversion
Convert string into zigzag pattern with given number of rows.

```python
def convert(s, num_rows):
    if num_rows == 1 or num_rows >= len(s):
        return s
    rows = [''] * num_rows
    cur, step = 0, 1
    for ch in s:
        rows[cur] += ch
        if cur == 0:
            step = 1
        elif cur == num_rows - 1:
            step = -1
        cur += step
    return ''.join(rows)

# Example
print(convert("PAYPALISHIRING", 3))  # Output: "PAHNAPLSIIGYIR"
```

## 13. Multiply Strings
Multiply two non-negative numbers represented as strings.

```python
def multiply(num1, num2):
    if num1 == "0" or num2 == "0":
        return "0"
    m, n = len(num1), len(num2)
    result = [0] * (m + n)
    for i in range(m - 1, -1, -1):
        for j in range(n - 1, -1, -1):
            mul = int(num1[i]) * int(num2[j])
            p1, p2 = i + j, i + j + 1
            total = mul + result[p2]
            result[p2] = total % 10
            result[p1] += total // 10
    return ''.join(map(str, result)).lstrip('0')

# Example
print(multiply("123", "456"))  # Output: "56088"
```

## 14. Decode String
Decode string of form k[encoded_string].

```python
def decode_string(s):
    stack = []
    cur_str = ""
    cur_num = 0
    for ch in s:
        if ch.isdigit():
            cur_num = cur_num * 10 + int(ch)
        elif ch == '[':
            stack.append((cur_str, cur_num))
            cur_str, cur_num = "", 0
        elif ch == ']':
            prev_str, num = stack.pop()
            cur_str = prev_str + cur_str * num
        else:
            cur_str += ch
    return cur_str

# Example
print(decode_string("3[a]2[bc]"))  # Output: "aaabcbc"
```

## 15. Generate Parentheses
Generate all combinations of n pairs of well-formed parentheses.

```python
def generate_parenthesis(n):
    result = []
    def backtrack(current, open_c, close_c):
        if len(current) == 2 * n:
            result.append(current)
            return
        if open_c < n:
            backtrack(current + '(', open_c + 1, close_c)
        if close_c < open_c:
            backtrack(current + ')', open_c, close_c + 1)
    backtrack("", 0, 0)
    return result

# Example
print(generate_parenthesis(3))
# Output: ['((()))','(()())','(())()','()(())','()()()']
```

---

# Recursion / Backtracking - Easy

## 1. Subsets
Generate all possible subsets of a set.

```python
def subsets(nums):
    result = []
    def backtrack(start, path):
        result.append(path[:])
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    backtrack(0, [])
    return result

# Example
print(subsets([1, 2, 3]))
# Output: [[],[1],[1,2],[1,2,3],[1,3],[2],[2,3],[3]]
```

## 2. Permutations
Generate all permutations of a list.

```python
def permute(nums):
    result = []
    def backtrack(path, used):
        if len(path) == len(nums):
            result.append(path[:])
            return
        for i in range(len(nums)):
            if not used[i]:
                used[i] = True
                path.append(nums[i])
                backtrack(path, used)
                path.pop()
                used[i] = False
    backtrack([], [False] * len(nums))
    return result

# Example
print(permute([1, 2, 3]))
# Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

## 3. Fibonacci using Recursion
Compute nth Fibonacci number.

```python
def fib(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib(n - 1, memo) + fib(n - 2, memo)
    return memo[n]

# Example
print(fib(10))  # Output: 55
```

## 4. Power Set
Print all subsets of a string.

```python
def power_set(s):
    result = []
    def backtrack(i, current):
        if i == len(s):
            result.append(current)
            return
        backtrack(i + 1, current + s[i])  # include
        backtrack(i + 1, current)         # exclude
    backtrack(0, "")
    return result

# Example
print(power_set("abc"))
# Output: ['abc','ab','ac','a','bc','b','c','']
```

## 5. Binary Search using Recursion
Search target in sorted array recursively.

```python
def binary_search(arr, target, low=0, high=None):
    if high is None:
        high = len(arr) - 1
    if low > high:
        return -1
    mid = (low + high) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search(arr, target, mid + 1, high)
    else:
        return binary_search(arr, target, low, mid - 1)

# Example
print(binary_search([1, 3, 5, 7, 9, 11], 7))  # Output: 3
```

---

# Recursion / Backtracking - Medium

## 1. Subsets II
Generate subsets of array containing duplicates (no duplicate subsets).

```python
def subsets_with_dup(nums):
    nums.sort()
    result = []
    def backtrack(start, path):
        result.append(path[:])
        for i in range(start, len(nums)):
            if i > start and nums[i] == nums[i-1]:
                continue
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    backtrack(0, [])
    return result

# Example
print(subsets_with_dup([1, 2, 2]))
# Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

## 2. Combination Sum
Find all unique combinations summing to target (each number unlimited use).

```python
def combination_sum(candidates, target):
    result = []
    def backtrack(start, path, total):
        if total == target:
            result.append(path[:])
            return
        if total > target:
            return
        for i in range(start, len(candidates)):
            path.append(candidates[i])
            backtrack(i, path, total + candidates[i])
            path.pop()
    backtrack(0, [], 0)
    return result

# Example
print(combination_sum([2, 3, 6, 7], 7))
# Output: [[2, 2, 3], [7]]
```

## 3. Combination Sum II
Each number used once, no duplicate combinations.

```python
def combination_sum2(candidates, target):
    candidates.sort()
    result = []
    def backtrack(start, path, total):
        if total == target:
            result.append(path[:])
            return
        if total > target:
            return
        for i in range(start, len(candidates)):
            if i > start and candidates[i] == candidates[i-1]:
                continue
            path.append(candidates[i])
            backtrack(i + 1, path, total + candidates[i])
            path.pop()
    backtrack(0, [], 0)
    return result

# Example
print(combination_sum2([10,1,2,7,6,1,5], 8))
# Output: [[1,1,6],[1,2,5],[1,7],[2,6]]
```

## 4. Permutation Sequence
Find kth permutation of numbers 1 to n.

```python
def get_permutation(n, k):
    import math
    nums = list(range(1, n + 1))
    k -= 1
    result = ""
    for i in range(n, 0, -1):
        idx, k = divmod(k, math.factorial(i - 1))
        result += str(nums.pop(idx))
    return result

# Example
print(get_permutation(3, 3))  # Output: "213"
```

## 5. Permutations II
Permutations with duplicates (return unique only).

```python
def permute_unique(nums):
    nums.sort()
    result = []
    used = [False] * len(nums)
    def backtrack(path):
        if len(path) == len(nums):
            result.append(path[:])
            return
        for i in range(len(nums)):
            if used[i]:
                continue
            if i > 0 and nums[i] == nums[i-1] and not used[i-1]:
                continue
            used[i] = True
            path.append(nums[i])
            backtrack(path)
            path.pop()
            used[i] = False
    backtrack([])
    return result

# Example
print(permute_unique([1, 1, 2]))
# Output: [[1,1,2],[1,2,1],[2,1,1]]
```

## 6. Letter Combinations of a Phone Number
Return all letter combinations for digit string.

```python
def letter_combinations(digits):
    if not digits:
        return []
    mapping = {'2':'abc','3':'def','4':'ghi','5':'jkl',
               '6':'mno','7':'pqrs','8':'tuv','9':'wxyz'}
    result = []
    def backtrack(i, current):
        if i == len(digits):
            result.append(current)
            return
        for ch in mapping[digits[i]]:
            backtrack(i + 1, current + ch)
    backtrack(0, "")
    return result

# Example
print(letter_combinations("23"))
# Output: ['ad','ae','af','bd','be','bf','cd','ce','cf']
```

## 7. Generate Parentheses
(See Strings - Medium #15 above)

## 8. Word Search
Find word in 2D board (adjacent cells, no reuse).

```python
def exist(board, word):
    rows, cols = len(board), len(board[0])
    def dfs(r, c, i):
        if i == len(word):
            return True
        if r < 0 or r >= rows or c < 0 or c >= cols or board[r][c] != word[i]:
            return False
        temp = board[r][c]
        board[r][c] = '#'
        found = (dfs(r+1,c,i+1) or dfs(r-1,c,i+1)
                 or dfs(r,c+1,i+1) or dfs(r,c-1,i+1))
        board[r][c] = temp
        return found
    for r in range(rows):
        for c in range(cols):
            if dfs(r, c, 0):
                return True
    return False

# Example
board = [['A','B','C','E'],['S','F','C','S'],['A','D','E','E']]
print(exist(board, "ABCCED"))  # Output: True
```

## 9. Palindrome Partitioning
(See Strings - Medium #9 above)

## 10. N-Queens
Place n queens on n x n board so they don't attack each other.

```python
def solve_n_queens(n):
    result = []
    board = [['.'] * n for _ in range(n)]
    cols, diag1, diag2 = set(), set(), set()
    def backtrack(row):
        if row == n:
            result.append([''.join(r) for r in board])
            return
        for col in range(n):
            if col in cols or (row - col) in diag1 or (row + col) in diag2:
                continue
            cols.add(col); diag1.add(row - col); diag2.add(row + col)
            board[row][col] = 'Q'
            backtrack(row + 1)
            cols.remove(col); diag1.remove(row - col); diag2.remove(row + col)
            board[row][col] = '.'
    backtrack(0)
    return result

# Example
print(solve_n_queens(4))
# Output: [['.Q..','...Q','Q...','..Q.'], ['..Q.','Q...','...Q','.Q..']]
```

## 11. Rat in a Maze
Find all paths from (0,0) to (n-1,n-1) in maze.

```python
def rat_maze(maze):
    n = len(maze)
    result = []
    visited = [[False] * n for _ in range(n)]
    def dfs(i, j, path):
        if i == n-1 and j == n-1:
            result.append(path)
            return
        moves = [('D',1,0), ('L',0,-1), ('R',0,1), ('U',-1,0)]
        visited[i][j] = True
        for d, di, dj in moves:
            ni, nj = i+di, j+dj
            if 0 <= ni < n and 0 <= nj < n and not visited[ni][nj] and maze[ni][nj] == 1:
                dfs(ni, nj, path + d)
        visited[i][j] = False
    if maze[0][0] == 1:
        dfs(0, 0, "")
    return sorted(result)

# Example
maze = [[1,0,0,0],[1,1,0,1],[1,1,0,0],[0,1,1,1]]
print(rat_maze(maze))  # Output: ['DDRDRR', 'DRDDRR']
```

## 12. Sudoku Solver
Fill empty cells of Sudoku so it becomes valid.

```python
def solve_sudoku(board):
    def is_valid(r, c, ch):
        for i in range(9):
            if board[r][i] == ch or board[i][c] == ch:
                return False
            if board[3*(r//3)+i//3][3*(c//3)+i%3] == ch:
                return False
        return True
    def backtrack():
        for r in range(9):
            for c in range(9):
                if board[r][c] == '.':
                    for ch in '123456789':
                        if is_valid(r, c, ch):
                            board[r][c] = ch
                            if backtrack():
                                return True
                            board[r][c] = '.'
                    return False
        return True
    backtrack()
    return board

# Example: pass a 9x9 board with '.' for empty cells.
```

## 13. Combination Sum III
Find all combinations of k numbers from 1-9 summing to n.

```python
def combination_sum3(k, n):
    result = []
    def backtrack(start, path, total):
        if len(path) == k and total == n:
            result.append(path[:])
            return
        if len(path) >= k or total >= n:
            return
        for i in range(start, 10):
            path.append(i)
            backtrack(i + 1, path, total + i)
            path.pop()
    backtrack(1, [], 0)
    return result

# Example
print(combination_sum3(3, 7))  # Output: [[1, 2, 4]]
```

## 14. Restore IP Addresses
Return all valid IP address combinations from string of digits.

```python
def restore_ip_addresses(s):
    result = []
    def backtrack(start, path):
        if len(path) == 4:
            if start == len(s):
                result.append('.'.join(path))
            return
        for length in range(1, 4):
            if start + length > len(s):
                break
            segment = s[start:start+length]
            if (segment.startswith('0') and len(segment) > 1) or int(segment) > 255:
                continue
            path.append(segment)
            backtrack(start + length, path)
            path.pop()
    backtrack(0, [])
    return result

# Example
print(restore_ip_addresses("25525511135"))
# Output: ['255.255.11.135', '255.255.111.35']
```

## 15. Flatten Nested List using Recursion
Flatten a deeply nested list (with mixed lists and tuples) into a single flat list using recursion.

```python
def flatten(nested):
    result = []
    for item in nested:
        # If item is a list or tuple, recurse into it
        if isinstance(item, (list, tuple)):
            result.extend(flatten(item))
        else:
            # Base case: it's a single number, just add it
            result.append(item)
    return result


# Example
nested = [1, 3, [4, 6, [56, 9, [9, 3]]], 8, (4, 2, 9)]
print(flatten(nested))
# Output: [1, 3, 4, 6, 56, 9, 9, 3, 8, 4, 2, 9]
```

---

# Tips for Interviews

1. **Explain your approach first** before coding — interviewers value clear thinking.
2. **Always state time and space complexity** after solving.
3. **Test with edge cases**: empty input, single element, all duplicates, negative numbers.
4. **Know multiple approaches** (brute force → optimized) for the same problem.
5. **Practice writing on paper or whiteboard** — many service company interviews still use this format.

**Good luck with your interviews!** 🚀
