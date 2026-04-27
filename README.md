# 🔥 Top 50 DSA Questions — Python Solutions
*Service-Based Companies Interview Prep*

> Solutions written with minimal use of Python built-ins (used only when necessary).

---

## 🔹 ARRAYS

### 1. Find Largest & Smallest Element
```python
def find_largest_smallest(arr):
    largest = arr[0]
    smallest = arr[0]
    for i in range(1, len(arr)):
        if arr[i] > largest:
            largest = arr[i]
        if arr[i] < smallest:
            smallest = arr[i]
    return largest, smallest

# Test
print(find_largest_smallest([3, 1, 9, 4, 7]))  # (9, 1)
```

### 2. Reverse an Array
```python
def reverse_array(arr):
    start = 0
    end = len(arr) - 1
    while start < end:
        arr[start], arr[end] = arr[end], arr[start]
        start += 1
        end -= 1
    return arr

# Test
print(reverse_array([1, 2, 3, 4, 5]))  # [5, 4, 3, 2, 1]
```

### 3. Find Second Largest Element
```python
def second_largest(arr):
    largest = -float('inf')
    second = -float('inf')
    for num in arr:
        if num > largest:
            second = largest
            largest = num
        elif num > second and num != largest:
            second = num
    return second

# Test
print(second_largest([10, 5, 8, 20, 20, 15]))  # 15
```

### 4. Move All Zeros to End
```python
def move_zeros(arr):
    pos = 0  # position to place next non-zero
    for i in range(len(arr)):
        if arr[i] != 0:
            arr[pos], arr[i] = arr[i], arr[pos]
            pos += 1
    return arr

# Test
print(move_zeros([0, 1, 0, 3, 12]))  # [1, 3, 12, 0, 0]
```

### 5. Remove Duplicates from Sorted Array
```python
def remove_duplicates(arr):
    if len(arr) == 0:
        return 0
    j = 0  # index of last unique element
    for i in range(1, len(arr)):
        if arr[i] != arr[j]:
            j += 1
            arr[j] = arr[i]
    return arr[:j+1]

# Test
print(remove_duplicates([1, 1, 2, 2, 3, 4, 4, 5]))  # [1, 2, 3, 4, 5]
```

### 6. Left Rotate Array by K Steps
```python
def reverse(arr, start, end):
    while start < end:
        arr[start], arr[end] = arr[end], arr[start]
        start += 1
        end -= 1

def left_rotate(arr, k):
    n = len(arr)
    k = k % n  # handle k > n
    reverse(arr, 0, k - 1)
    reverse(arr, k, n - 1)
    reverse(arr, 0, n - 1)
    return arr

# Test
print(left_rotate([1, 2, 3, 4, 5], 2))  # [3, 4, 5, 1, 2]
```

### 7. Find Missing Number (1 to N)
```python
def find_missing(arr, n):
    # Sum of 1 to n = n*(n+1)/2
    expected_sum = n * (n + 1) // 2
    actual_sum = 0
    for num in arr:
        actual_sum += num
    return expected_sum - actual_sum

# Test
print(find_missing([1, 2, 4, 5, 6], 6))  # 3
```

### 8. Find Duplicate Element
```python
def find_duplicate(arr):
    seen = set()
    for num in arr:
        if num in seen:
            return num
        seen.add(num)
    return -1

# Test
print(find_duplicate([1, 3, 4, 2, 2]))  # 2
```

### 9. Kadane's Algorithm (Maximum Subarray Sum)
```python
def max_subarray_sum(arr):
    max_sum = arr[0]
    current_sum = arr[0]
    for i in range(1, len(arr)):
        if current_sum < 0:
            current_sum = arr[i]
        else:
            current_sum += arr[i]
        if current_sum > max_sum:
            max_sum = current_sum
    return max_sum

# Test
print(max_subarray_sum([-2, 1, -3, 4, -1, 2, 1, -5, 4]))  # 6
```

### 10. Two Sum Problem
```python
def two_sum(arr, target):
    seen = {}  # value -> index
    for i in range(len(arr)):
        complement = target - arr[i]
        if complement in seen:
            return [seen[complement], i]
        seen[arr[i]] = i
    return []

# Test
print(two_sum([2, 7, 11, 15], 9))  # [0, 1]
```

---

## 🔹 STRINGS

### 1. Reverse a String
```python
def reverse_string(s):
    chars = list(s)
    start = 0
    end = len(chars) - 1
    while start < end:
        chars[start], chars[end] = chars[end], chars[start]
        start += 1
        end -= 1
    # Build result manually
    result = ""
    for ch in chars:
        result += ch
    return result

# Test
print(reverse_string("hello"))  # olleh
```

### 2. Check Palindrome String
```python
def is_palindrome(s):
    start = 0
    end = len(s) - 1
    while start < end:
        if s[start] != s[end]:
            return False
        start += 1
        end -= 1
    return True

# Test
print(is_palindrome("madam"))  # True
print(is_palindrome("hello"))  # False
```

### 3. Count Vowels & Consonants
```python
def count_vowels_consonants(s):
    vowels = 0
    consonants = 0
    for ch in s:
        # Convert to lowercase manually
        if 'A' <= ch <= 'Z':
            ch = chr(ord(ch) + 32)
        if 'a' <= ch <= 'z':
            if ch == 'a' or ch == 'e' or ch == 'i' or ch == 'o' or ch == 'u':
                vowels += 1
            else:
                consonants += 1
    return vowels, consonants

# Test
print(count_vowels_consonants("Hello World"))  # (3, 7)
```

### 4. Remove Spaces from String
```python
def remove_spaces(s):
    result = ""
    for ch in s:
        if ch != ' ':
            result += ch
    return result

# Test
print(remove_spaces("Hello World Python"))  # HelloWorldPython
```

### 5. Anagram Check
```python
def are_anagrams(s1, s2):
    if len(s1) != len(s2):
        return False
    
    # Count characters using array of size 26
    count = [0] * 26
    for ch in s1:
        count[ord(ch) - ord('a')] += 1
    for ch in s2:
        count[ord(ch) - ord('a')] -= 1
    
    for c in count:
        if c != 0:
            return False
    return True

# Test
print(are_anagrams("listen", "silent"))  # True
print(are_anagrams("hello", "world"))    # False
```

### 6. First Non-Repeating Character
```python
def first_non_repeating(s):
    count = {}
    for ch in s:
        if ch in count:
            count[ch] += 1
        else:
            count[ch] = 1
    
    for ch in s:
        if count[ch] == 1:
            return ch
    return None

# Test
print(first_non_repeating("aabbcdd"))  # c
```

### 7. String Compression (aaabb → a3b2)
```python
def compress_string(s):
    if len(s) == 0:
        return ""
    
    result = ""
    count = 1
    for i in range(1, len(s)):
        if s[i] == s[i-1]:
            count += 1
        else:
            result += s[i-1] + str(count)
            count = 1
    result += s[-1] + str(count)
    return result

# Test
print(compress_string("aaabbc"))  # a3b2c1
```

### 8. Longest Common Prefix
```python
def longest_common_prefix(strs):
    if len(strs) == 0:
        return ""
    
    prefix = strs[0]
    for i in range(1, len(strs)):
        # Reduce prefix until it matches start of strs[i]
        j = 0
        while j < len(prefix) and j < len(strs[i]) and prefix[j] == strs[i][j]:
            j += 1
        prefix = prefix[:j]
        if prefix == "":
            return ""
    return prefix

# Test
print(longest_common_prefix(["flower", "flow", "flight"]))  # fl
```

---

## 🔹 LINKED LIST

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
```

### 1. Reverse a Linked List
```python
def reverse_linked_list(head):
    prev = None
    current = head
    while current is not None:
        next_node = current.next
        current.next = prev
        prev = current
        current = next_node
    return prev

# Helper to print
def print_list(head):
    while head:
        print(head.data, end=" -> ")
        head = head.next
    print("None")

# Test
head = Node(1); head.next = Node(2); head.next.next = Node(3)
new_head = reverse_linked_list(head)
print_list(new_head)  # 3 -> 2 -> 1 -> None
```

### 2. Detect Loop in Linked List (Floyd's Algorithm)
```python
def has_loop(head):
    slow = head
    fast = head
    while fast is not None and fast.next is not None:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

### 3. Find Middle of Linked List
```python
def find_middle(head):
    slow = head
    fast = head
    while fast is not None and fast.next is not None:
        slow = slow.next
        fast = fast.next.next
    return slow

# Test
head = Node(1); head.next = Node(2); head.next.next = Node(3)
head.next.next.next = Node(4); head.next.next.next.next = Node(5)
print(find_middle(head).data)  # 3
```

### 4. Merge Two Sorted Linked Lists
```python
def merge_sorted_lists(l1, l2):
    dummy = Node(0)
    tail = dummy
    
    while l1 is not None and l2 is not None:
        if l1.data <= l2.data:
            tail.next = l1
            l1 = l1.next
        else:
            tail.next = l2
            l2 = l2.next
        tail = tail.next
    
    if l1 is not None:
        tail.next = l1
    if l2 is not None:
        tail.next = l2
    
    return dummy.next
```

### 5. Remove Nth Node from End
```python
def remove_nth_from_end(head, n):
    dummy = Node(0)
    dummy.next = head
    fast = dummy
    slow = dummy
    
    # Move fast n+1 steps ahead
    for _ in range(n + 1):
        fast = fast.next
    
    # Move both until fast reaches end
    while fast is not None:
        slow = slow.next
        fast = fast.next
    
    # Remove the node
    slow.next = slow.next.next
    return dummy.next
```

---

## 🔹 STACK & QUEUE

### 1. Implement Stack Using Array
```python
class Stack:
    def __init__(self, capacity=100):
        self.arr = [0] * capacity
        self.top = -1
        self.capacity = capacity
    
    def push(self, value):
        if self.top == self.capacity - 1:
            print("Stack Overflow")
            return
        self.top += 1
        self.arr[self.top] = value
    
    def pop(self):
        if self.top == -1:
            print("Stack Underflow")
            return None
        value = self.arr[self.top]
        self.top -= 1
        return value
    
    def peek(self):
        if self.top == -1:
            return None
        return self.arr[self.top]
    
    def is_empty(self):
        return self.top == -1

# Test
s = Stack()
s.push(10); s.push(20); s.push(30)
print(s.pop())   # 30
print(s.peek())  # 20
```

### 2. Valid Parentheses
```python
def is_valid_parentheses(s):
    stack = []
    pairs = {')': '(', '}': '{', ']': '['}
    
    for ch in s:
        if ch == '(' or ch == '{' or ch == '[':
            stack.append(ch)
        elif ch == ')' or ch == '}' or ch == ']':
            if len(stack) == 0:
                return False
            if stack[-1] != pairs[ch]:
                return False
            stack.pop()
    return len(stack) == 0

# Test
print(is_valid_parentheses("({[]})"))  # True
print(is_valid_parentheses("({[})"))   # False
```

### 3. Next Greater Element
```python
def next_greater_element(arr):
    n = len(arr)
    result = [-1] * n
    stack = []  # stack of indices
    
    for i in range(n):
        while len(stack) > 0 and arr[stack[-1]] < arr[i]:
            idx = stack.pop()
            result[idx] = arr[i]
        stack.append(i)
    return result

# Test
print(next_greater_element([4, 5, 2, 25]))  # [5, 25, 25, -1]
```

### 4. Implement Queue Using Array
```python
class Queue:
    def __init__(self, capacity=100):
        self.arr = [0] * capacity
        self.front = 0
        self.rear = -1
        self.size = 0
        self.capacity = capacity
    
    def enqueue(self, value):
        if self.size == self.capacity:
            print("Queue Overflow")
            return
        self.rear = (self.rear + 1) % self.capacity
        self.arr[self.rear] = value
        self.size += 1
    
    def dequeue(self):
        if self.size == 0:
            print("Queue Underflow")
            return None
        value = self.arr[self.front]
        self.front = (self.front + 1) % self.capacity
        self.size -= 1
        return value
    
    def is_empty(self):
        return self.size == 0

# Test
q = Queue()
q.enqueue(1); q.enqueue(2); q.enqueue(3)
print(q.dequeue())  # 1
print(q.dequeue())  # 2
```

### 5. Reverse a Queue (using stack)
```python
def reverse_queue(q):
    stack = []
    while not q.is_empty():
        stack.append(q.dequeue())
    while len(stack) > 0:
        q.enqueue(stack.pop())
    return q
```

---

## 🔹 RECURSION / BASIC DP

### 1. Factorial Using Recursion
```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)

# Test
print(factorial(5))  # 120
```

### 2. Fibonacci (Recursive + DP)
```python
# Recursive (slow)
def fib_recursive(n):
    if n <= 1:
        return n
    return fib_recursive(n - 1) + fib_recursive(n - 2)

# DP (efficient)
def fib_dp(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]

# Optimized (O(1) space)
def fib_optimized(n):
    if n <= 1:
        return n
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b

# Test
print(fib_dp(10))  # 55
```

### 3. Power of Number (x^n)
```python
def power(x, n):
    if n == 0:
        return 1
    if n < 0:
        return 1 / power(x, -n)
    
    # Fast exponentiation: O(log n)
    half = power(x, n // 2)
    if n % 2 == 0:
        return half * half
    else:
        return half * half * x

# Test
print(power(2, 10))  # 1024
```

### 4. Climbing Stairs Problem
```python
def climb_stairs(n):
    if n <= 2:
        return n
    a, b = 1, 2
    for _ in range(3, n + 1):
        a, b = b, a + b
    return b

# Test
print(climb_stairs(5))  # 8
```

---

## 🔹 SEARCHING & SORTING

### 1. Binary Search
```python
def binary_search(arr, target):
    low = 0
    high = len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

# Test
print(binary_search([1, 3, 5, 7, 9, 11], 7))  # 3
```

### 2. Bubble Sort
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr

# Test
print(bubble_sort([64, 34, 25, 12, 22, 11, 90]))
```

### 3. Selection Sort
```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr

# Test
print(selection_sort([64, 25, 12, 22, 11]))
```

### 4. Insertion Sort
```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

# Test
print(insertion_sort([12, 11, 13, 5, 6]))
```

### 5. Merge Sort
```python
def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    while i < len(left):
        result.append(left[i])
        i += 1
    while j < len(right):
        result.append(right[j])
        j += 1
    return result

def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

# Test
print(merge_sort([38, 27, 43, 3, 9, 82, 10]))
```

---

## 🔹 MATRIX PROBLEMS

### 1. Print Matrix in Spiral Form
```python
def spiral_order(matrix):
    if len(matrix) == 0:
        return []
    
    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1
    
    while top <= bottom and left <= right:
        # Top row
        for i in range(left, right + 1):
            result.append(matrix[top][i])
        top += 1
        
        # Right column
        for i in range(top, bottom + 1):
            result.append(matrix[i][right])
        right -= 1
        
        # Bottom row
        if top <= bottom:
            for i in range(right, left - 1, -1):
                result.append(matrix[bottom][i])
            bottom -= 1
        
        # Left column
        if left <= right:
            for i in range(bottom, top - 1, -1):
                result.append(matrix[i][left])
            left += 1
    return result

# Test
matrix = [[1,2,3],[4,5,6],[7,8,9]]
print(spiral_order(matrix))  # [1, 2, 3, 6, 9, 8, 7, 4, 5]
```

### 2. Transpose of Matrix
```python
def transpose(matrix):
    rows = len(matrix)
    cols = len(matrix[0])
    result = [[0] * rows for _ in range(cols)]
    
    for i in range(rows):
        for j in range(cols):
            result[j][i] = matrix[i][j]
    return result

# Test
print(transpose([[1, 2, 3], [4, 5, 6]]))  # [[1, 4], [2, 5], [3, 6]]
```

### 3. Rotate Matrix 90 Degrees (Clockwise)
```python
def rotate_90(matrix):
    n = len(matrix)
    
    # Step 1: Transpose
    for i in range(n):
        for j in range(i + 1, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    
    # Step 2: Reverse each row
    for i in range(n):
        start, end = 0, n - 1
        while start < end:
            matrix[i][start], matrix[i][end] = matrix[i][end], matrix[i][start]
            start += 1
            end -= 1
    return matrix

# Test
m = [[1,2,3],[4,5,6],[7,8,9]]
print(rotate_90(m))  # [[7,4,1],[8,5,2],[9,6,3]]
```

---

## 🔹 BASIC MATH / LOGIC

### 1. Prime Number Check
```python
def is_prime(n):
    if n < 2:
        return False
    if n == 2:
        return True
    if n % 2 == 0:
        return False
    
    i = 3
    while i * i <= n:
        if n % i == 0:
            return False
        i += 2
    return True

# Test
print(is_prime(17))  # True
print(is_prime(15))  # False
```

### 2. GCD / HCF (Euclidean Algorithm)
```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

# Test
print(gcd(48, 18))  # 6
```

### 3. Armstrong Number
```python
def is_armstrong(n):
    # Count digits
    temp = n
    digits = 0
    while temp > 0:
        digits += 1
        temp //= 10
    
    # Calculate sum of digits raised to power
    temp = n
    total = 0
    while temp > 0:
        d = temp % 10
        # d^digits without using **
        power_val = 1
        for _ in range(digits):
            power_val *= d
        total += power_val
        temp //= 10
    
    return total == n

# Test
print(is_armstrong(153))  # True (1^3 + 5^3 + 3^3 = 153)
print(is_armstrong(123))  # False
```

### 4. Palindrome Number
```python
def is_palindrome_number(n):
    if n < 0:
        return False
    
    original = n
    reversed_num = 0
    while n > 0:
        digit = n % 10
        reversed_num = reversed_num * 10 + digit
        n //= 10
    return original == reversed_num

# Test
print(is_palindrome_number(121))  # True
print(is_palindrome_number(123))  # False
```

### 5. Count Digits in Number
```python
def count_digits(n):
    if n == 0:
        return 1
    
    if n < 0:
        n = -n
    
    count = 0
    while n > 0:
        count += 1
        n //= 10
    return count

# Test
print(count_digits(12345))  # 5
print(count_digits(0))      # 1
```

---

## 🔹 TREES (BASIC)

```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
```

### 1. Inorder Traversal
```python
def inorder(root):
    if root is None:
        return
    inorder(root.left)
    print(root.data, end=" ")
    inorder(root.right)

# Iterative version
def inorder_iterative(root):
    stack = []
    current = root
    result = []
    while current is not None or len(stack) > 0:
        while current is not None:
            stack.append(current)
            current = current.left
        current = stack.pop()
        result.append(current.data)
        current = current.right
    return result

# Test
root = TreeNode(1)
root.left = TreeNode(2); root.right = TreeNode(3)
root.left.left = TreeNode(4); root.left.right = TreeNode(5)
inorder(root)  # 4 2 5 1 3
```

### 2. Height of Binary Tree
```python
def height(root):
    if root is None:
        return 0
    left_height = height(root.left)
    right_height = height(root.right)
    if left_height > right_height:
        return left_height + 1
    else:
        return right_height + 1

# Test
print(height(root))  # 3
```

### 3. Count Nodes in Tree
```python
def count_nodes(root):
    if root is None:
        return 0
    return 1 + count_nodes(root.left) + count_nodes(root.right)

# Test
print(count_nodes(root))  # 5
```

---

## 🔹 GRAPH

### 1. BFS Traversal
```python
def bfs(graph, start):
    visited = set()
    queue = [start]
    visited.add(start)
    result = []
    
    while len(queue) > 0:
        node = queue.pop(0)  # dequeue from front
        result.append(node)
        
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    return result

# Test
graph = {
    0: [1, 2],
    1: [0, 3, 4],
    2: [0, 4],
    3: [1, 5],
    4: [1, 2, 5],
    5: [3, 4]
}
print(bfs(graph, 0))  # [0, 1, 2, 3, 4, 5]
```

### 2. DFS Traversal
```python
def dfs(graph, start, visited=None, result=None):
    if visited is None:
        visited = set()
    if result is None:
        result = []
    
    visited.add(start)
    result.append(start)
    
    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited, result)
    return result

# Iterative DFS using stack
def dfs_iterative(graph, start):
    visited = set()
    stack = [start]
    result = []
    
    while len(stack) > 0:
        node = stack.pop()
        if node not in visited:
            visited.add(node)
            result.append(node)
            # Push neighbors in reverse for left-to-right traversal
            for neighbor in graph[node]:
                if neighbor not in visited:
                    stack.append(neighbor)
    return result

# Test
print(dfs(graph, 0))  # [0, 1, 3, 5, 4, 2]
```

---

## 🎯 INTERVIEW TIPS

1. **Always explain your approach BEFORE coding** — interviewers value clarity of thought.
2. **Discuss time and space complexity** for every solution.
3. **Handle edge cases**: empty input, single element, negatives, duplicates, overflow.
4. **Dry run** your code with a sample input on paper.
5. **Start with brute force**, then optimize if asked.

## ⏱️ Complexity Cheat Sheet

| Algorithm | Time | Space |
|-----------|------|-------|
| Binary Search | O(log n) | O(1) |
| Bubble/Selection/Insertion Sort | O(n²) | O(1) |
| Merge Sort | O(n log n) | O(n) |
| Kadane's Algorithm | O(n) | O(1) |
| BFS / DFS | O(V + E) | O(V) |
| Tree Traversal | O(n) | O(h) |
| Floyd's Cycle Detection | O(n) | O(1) |

---

**Best of luck with your interviews! 🚀**
