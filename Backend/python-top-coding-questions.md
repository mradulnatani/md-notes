Yes. Since you're preparing for **Python interviews and DevOps/backend placements**, I’d structure the 50 problems from **easy → medium → interview-level**, and focus on patterns rather than random questions.

# 50 Python Coding Interview Problems With Solutions

## Level 1 — Basic Python Problems

### 1. Reverse a string

**Problem:** Reverse `"hello"` without using a loop.

```python
def reverse_string(s):
    return s[::-1]

print(reverse_string("hello"))
```

**Output:**

```text
olleh
```

**Concept:** String slicing.

**Time:** `O(n)`
**Space:** `O(n)`

---

### 2. Check if a string is a palindrome

```python
def is_palindrome(s):
    return s == s[::-1]

print(is_palindrome("madam"))
```

**Output:**

```text
True
```

**Concept:** Slicing.

---

### 3. Find the factorial of a number

```python
def factorial(n):
    result = 1

    for i in range(2, n + 1):
        result *= i

    return result

print(factorial(5))
```

**Output:**

```text
120
```

**Time:** `O(n)`
**Space:** `O(1)`

---

### 4. Find Fibonacci numbers

```python
def fibonacci(n):
    a, b = 0, 1

    for _ in range(n):
        print(a, end=" ")
        a, b = b, a + b

fibonacci(7)
```

**Output:**

```text
0 1 1 2 3 5 8
```

**Important:** Don't implement Fibonacci using naive recursion in an interview unless specifically asked. It has exponential time complexity.

---

### 5. Check whether a number is prime

```python
def is_prime(n):
    if n < 2:
        return False

    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False

    return True

print(is_prime(17))
```

**Output:**

```text
True
```

**Why only up to √n?**

If `n` has a factor greater than √n, its corresponding factor must be smaller than √n.

**Time:** `O(√n)`

---

### 6. Find the largest element in a list

```python
def find_max(numbers):
    maximum = numbers[0]

    for num in numbers:
        if num > maximum:
            maximum = num

    return maximum

print(find_max([10, 4, 25, 7, 18]))
```

**Output:**

```text
25
```

**Time:** `O(n)`

---

### 7. Find the smallest element

```python
def find_min(numbers):
    minimum = numbers[0]

    for num in numbers:
        if num < minimum:
            minimum = num

    return minimum
```

---

### 8. Find the sum of list elements

```python
def list_sum(numbers):
    total = 0

    for num in numbers:
        total += num

    return total

print(list_sum([1, 2, 3, 4, 5]))
```

**Output:**

```text
15
```

---

### 9. Count vowels in a string

```python
def count_vowels(s):
    vowels = "aeiou"
    count = 0

    for char in s.lower():
        if char in vowels:
            count += 1

    return count

print(count_vowels("Python Programming"))
```

---

### 10. Find whether a number is Armstrong

An Armstrong number is equal to the sum of its digits raised to the power of the number of digits.

For example:

```text
153 = 1³ + 5³ + 3³
```

```python
def is_armstrong(n):
    digits = str(n)
    power = len(digits)

    total = sum(int(digit) ** power for digit in digits)

    return total == n

print(is_armstrong(153))
```

**Output:**

```text
True
```

---

# Level 2 — Strings and Hashing

### 11. Count character frequency

```python
def frequency(s):
    result = {}

    for char in s:
        result[char] = result.get(char, 0) + 1

    return result

print(frequency("banana"))
```

**Output:**

```text
{'b': 1, 'a': 3, 'n': 2}
```

**Important interview pattern:** Hash map / dictionary.

**Time:** `O(n)`

---

### 12. Find the first non-repeating character

```python
def first_unique(s):
    frequency = {}

    for char in s:
        frequency[char] = frequency.get(char, 0) + 1

    for char in s:
        if frequency[char] == 1:
            return char

    return None

print(first_unique("swiss"))
```

**Output:**

```text
w
```

**Pattern:** Frequency map.

---

### 13. Check whether two strings are anagrams

```python
def is_anagram(s1, s2):
    return sorted(s1) == sorted(s2)

print(is_anagram("listen", "silent"))
```

**Output:**

```text
True
```

A better `O(n)` approach:

```python
from collections import Counter

def is_anagram(s1, s2):
    return Counter(s1) == Counter(s2)
```

---

### 14. Remove duplicate characters

```python
def remove_duplicates(s):
    result = ""

    for char in s:
        if char not in result:
            result += char

    return result

print(remove_duplicates("programming"))
```

A more efficient approach:

```python
def remove_duplicates(s):
    return "".join(dict.fromkeys(s))
```

---

### 15. Find duplicate characters

```python
def duplicates(s):
    frequency = {}

    for char in s:
        frequency[char] = frequency.get(char, 0) + 1

    return [char for char, count in frequency.items() if count > 1]

print(duplicates("programming"))
```

---

### 16. Reverse words in a sentence

Input:

```text
"Python is powerful"
```

Output:

```text
"powerful is Python"
```

Solution:

```python
def reverse_words(sentence):
    return " ".join(sentence.split()[::-1])

print(reverse_words("Python is powerful"))
```

---

### 17. Find the longest word

```python
def longest_word(sentence):
    words = sentence.split()
    return max(words, key=len)

print(longest_word("Python is extremely powerful"))
```

**Output:**

```text
extremely
```

---

### 18. Count words in a sentence

```python
def word_count(sentence):
    return len(sentence.split())

print(word_count("Python is easy to learn"))
```

**Output:**

```text
5
```

---

### 19. Find the most frequent character

```python
from collections import Counter

def most_frequent(s):
    return Counter(s).most_common(1)[0]

print(most_frequent("banana"))
```

**Output:**

```text
('a', 3)
```

---

### 20. Check if a string contains only digits

```python
def only_digits(s):
    return s.isdigit()

print(only_digits("12345"))
```

**Output:**

```text
True
```

Be aware that `isdigit()` recognizes more than just ASCII `0-9`; for strict ASCII validation, use an appropriate explicit check.

---

# Level 3 — Arrays / Lists

### 21. Remove duplicates from a list

```python
def remove_duplicates(numbers):
    return list(dict.fromkeys(numbers))

print(remove_duplicates([1, 2, 2, 3, 1, 4]))
```

**Output:**

```text
[1, 2, 3, 4]
```

This preserves insertion order.

---

### 22. Find the second-largest element

```python
def second_largest(numbers):
    unique = list(set(numbers))
    unique.sort()

    return unique[-2]

print(second_largest([10, 20, 5, 30, 20]))
```

**Output:**

```text
20
```

A more efficient one-pass solution:

```python
def second_largest(numbers):
    largest = second = float("-inf")

    for num in numbers:
        if num > largest:
            second = largest
            largest = num
        elif largest > num > second:
            second = num

    return second
```

---

### 23. Find common elements between two lists

```python
def common_elements(a, b):
    return list(set(a) & set(b))

print(common_elements([1, 2, 3, 4], [3, 4, 5, 6]))
```

**Output:**

```text
[3, 4]
```

---

### 24. Find missing number

Given:

```text
[1, 2, 3, 5]
```

Find `4`.

```python
def missing_number(numbers):
    n = len(numbers) + 1
    expected = n * (n + 1) // 2

    return expected - sum(numbers)

print(missing_number([1, 2, 3, 5]))
```

**Output:**

```text
4
```

---

### 25. Find duplicate number

```python
def find_duplicate(numbers):
    seen = set()

    for num in numbers:
        if num in seen:
            return num

        seen.add(num)

print(find_duplicate([1, 3, 4, 2, 2]))
```

**Output:**

```text
2
```

**Pattern:** Hash set.

---

### 26. Move all zeros to the end

Input:

```text
[0, 1, 0, 3, 12]
```

Output:

```text
[1, 3, 12, 0, 0]
```

```python
def move_zeros(numbers):
    result = [x for x in numbers if x != 0]
    result.extend([0] * (len(numbers) - len(result)))

    return result

print(move_zeros([0, 1, 0, 3, 12]))
```

---

### 27. Find the intersection of two arrays

```python
def intersection(a, b):
    return list(set(a).intersection(b))

print(intersection([1, 2, 2, 3], [2, 2, 4]))
```

---

### 28. Find pairs that sum to a target

Input:

```text
[2, 7, 11, 15]
target = 9
```

Output:

```text
(2, 7)
```

```python
def two_sum(numbers, target):
    seen = set()

    for num in numbers:
        complement = target - num

        if complement in seen:
            return complement, num

        seen.add(num)

    return None

print(two_sum([2, 7, 11, 15], 9))
```

**Time:** `O(n)`
**Space:** `O(n)`

This is one of the **most important interview patterns**.

---

### 29. Find maximum subarray sum

This is the famous **Kadane's Algorithm**.

```python
def max_subarray(numbers):
    current = maximum = numbers[0]

    for num in numbers[1:]:
        current = max(num, current + num)
        maximum = max(maximum, current)

    return maximum

print(max_subarray([-2, 1, -3, 4, -1, 2, 1, -5, 4]))
```

**Output:**

```text
6
```

The maximum subarray is:

```text
[4, -1, 2, 1]
```

**Time:** `O(n)`

---

### 30. Rotate an array by k positions

```python
def rotate(numbers, k):
    k %= len(numbers)

    return numbers[-k:] + numbers[:-k]

print(rotate([1, 2, 3, 4, 5], 2))
```

Output:

```text
[4, 5, 1, 2, 3]
```

---

# Level 4 — Searching and Sorting

### 31. Implement linear search

```python
def linear_search(numbers, target):
    for i, num in enumerate(numbers):
        if num == target:
            return i

    return -1

print(linear_search([10, 20, 30, 40], 30))
```

Output:

```text
2
```

**Time:** `O(n)`

---

### 32. Implement binary search

The array must be sorted.

```python
def binary_search(numbers, target):
    left = 0
    right = len(numbers) - 1

    while left <= right:
        mid = (left + right) // 2

        if numbers[mid] == target:
            return mid

        if numbers[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

**Time:** `O(log n)`

This is an extremely important interview algorithm.

---

### 33. Implement bubble sort

```python
def bubble_sort(numbers):
    n = len(numbers)

    for i in range(n):
        swapped = False

        for j in range(0, n - i - 1):
            if numbers[j] > numbers[j + 1]:
                numbers[j], numbers[j + 1] = numbers[j + 1], numbers[j]
                swapped = True

        if not swapped:
            break

    return numbers

print(bubble_sort([5, 2, 8, 1, 3]))
```

**Average time:** `O(n²)`

---

### 34. Implement selection sort

```python
def selection_sort(numbers):
    n = len(numbers)

    for i in range(n):
        minimum = i

        for j in range(i + 1, n):
            if numbers[j] < numbers[minimum]:
                minimum = j

        numbers[i], numbers[minimum] = numbers[minimum], numbers[i]

    return numbers
```

**Time:** `O(n²)`

---

### 35. Find the kth largest element

```python
def kth_largest(numbers, k):
    numbers.sort(reverse=True)

    return numbers[k - 1]

print(kth_largest([3, 2, 1, 5, 6, 4], 2))
```

Output:

```text
5
```

For large inputs, an interviewer may expect a **heap** or **quickselect** solution rather than sorting the entire array.

---

# Level 5 — Dictionaries and Data Structures

### 36. Group anagrams

Input:

```text
["eat", "tea", "tan", "ate", "nat", "bat"]
```

Output conceptually:

```text
[
    ["eat", "tea", "ate"],
    ["tan", "nat"],
    ["bat"]
]
```

Solution:

```python
from collections import defaultdict

def group_anagrams(words):
    groups = defaultdict(list)

    for word in words:
        key = tuple(sorted(word))
        groups[key].append(word)

    return list(groups.values())

print(group_anagrams(
    ["eat", "tea", "tan", "ate", "nat", "bat"]
))
```

**Pattern:** Hash map.

---

### 37. Find the top K frequent elements

```python
from collections import Counter

def top_k(numbers, k):
    return [item for item, count in Counter(numbers).most_common(k)]

print(top_k([1, 1, 1, 2, 2, 3], 2))
```

Output:

```text
[1, 2]
```

For large inputs, know the heap-based approach.

---

### 38. Merge two dictionaries

```python
def merge_dicts(a, b):
    return {**a, **b}

a = {"a": 1, "b": 2}
b = {"c": 3, "d": 4}

print(merge_dicts(a, b))
```

In modern Python, you can also use:

```python
merged = a | b
```

If duplicate keys exist, values from the right-hand dictionary win.

---

### 39. Invert a dictionary

Input:

```python
{"a": 1, "b": 2}
```

Output:

```python
{1: "a", 2: "b"}
```

```python
def invert_dictionary(d):
    return {value: key for key, value in d.items()}
```

This assumes the values are unique and hashable.

---

### 40. Find the highest-value key

```python
def highest_value_key(d):
    return max(d, key=d.get)

data = {
    "a": 10,
    "b": 50,
    "c": 30
}

print(highest_value_key(data))
```

Output:

```text
b
```

---

# Level 6 — Stack, Queue and Linked-List Patterns

### 41. Check balanced parentheses

Input:

```text
"{[()]}"
```

Output:

```text
True
```

```python
def balanced_parentheses(s):
    stack = []
    pairs = {
        ")": "(",
        "]": "[",
        "}": "{"
    }

    for char in s:
        if char in "([{":
            stack.append(char)

        elif char in ")]}":
            if not stack or stack.pop() != pairs[char]:
                return False

    return len(stack) == 0

print(balanced_parentheses("{[()]}"))
```

**Pattern:** Stack.

**Time:** `O(n)`

---

### 42. Implement a stack

Python's list works well as a stack.

```python
class Stack:

    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if not self.items:
            return None

        return self.items.pop()

    def peek(self):
        if not self.items:
            return None

        return self.items[-1]

    def is_empty(self):
        return len(self.items) == 0
```

---

### 43. Implement a queue

For an actual queue, prefer `collections.deque` rather than repeatedly using `list.pop(0)`.

```python
from collections import deque

class Queue:

    def __init__(self):
        self.items = deque()

    def enqueue(self, item):
        self.items.append(item)

    def dequeue(self):
        if not self.items:
            return None

        return self.items.popleft()
```

`deque` gives efficient operations at both ends.

---

### 44. Reverse a linked list

```python
class Node:

    def __init__(self, value):
        self.value = value
        self.next = None


def reverse_linked_list(head):
    previous = None
    current = head

    while current:
        next_node = current.next
        current.next = previous
        previous = current
        current = next_node

    return previous
```

The important idea is:

```text
previous ← current ← next
```

and then move through the list.

**Time:** `O(n)`
**Space:** `O(1)`

---

### 45. Detect a cycle in a linked list

Use **Floyd's cycle detection algorithm**.

```python
def has_cycle(head):
    slow = head
    fast = head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

        if slow is fast:
            return True

    return False
```

**Time:** `O(n)`
**Space:** `O(1)`

---

# Level 7 — Recursion / Trees / Graphs

### 46. Calculate power using recursion

```python
def power(x, n):
    if n == 0:
        return 1

    return x * power(x, n - 1)

print(power(2, 5))
```

Output:

```text
32
```

For a serious interview, you should also know **fast exponentiation**, which reduces the time from `O(n)` to `O(log n)`.

---

### 47. Binary tree inorder traversal

```python
class TreeNode:

    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None


def inorder(root):
    if root is None:
        return

    inorder(root.left)
    print(root.value)
    inorder(root.right)
```

For:

```text
       1
      / \
     2   3
```

Output:

```text
2
1
3
```

Remember:

```text
INORDER = LEFT → ROOT → RIGHT
```

---

### 48. Find the height of a binary tree

```python
def height(root):
    if root is None:
        return 0

    return 1 + max(
        height(root.left),
        height(root.right)
    )
```

For:

```text
       1
      / \
     2   3
    /
   4
```

height = `3` if counting nodes.

---

### 49. Breadth-first search (BFS)

For a graph:

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])

    while queue:
        node = queue.popleft()

        if node in visited:
            continue

        visited.add(node)
        print(node)

        for neighbor in graph[node]:
            if neighbor not in visited:
                queue.append(neighbor)
```

Example graph:

```python
graph = {
    "A": ["B", "C"],
    "B": ["D"],
    "C": ["E"],
    "D": [],
    "E": []
}
```

```python
bfs(graph, "A")
```

Possible output:

```text
A
B
C
D
E
```

**Pattern:** Queue.

---

### 50. Depth-first search (DFS)

Recursive DFS:

```python
def dfs(graph, node, visited=None):

    if visited is None:
        visited = set()

    if node in visited:
        return

    visited.add(node)
    print(node)

    for neighbor in graph[node]:
        dfs(graph, neighbor, visited)
```

Example:

```python
graph = {
    "A": ["B", "C"],
    "B": ["D"],
    "C": ["E"],
    "D": [],
    "E": []
}

dfs(graph, "A")
```

Possible output:

```text
A
B
D
C
E
```

**Pattern:** Recursion / stack.

---

