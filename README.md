# LeetCode-1081---Smallest-Subsequence-of-Distinct-Characters
Java solution for LeetCode 1081 - Smallest Subsequence of Distinct Characters using a Greedy Algorithm and Monotonic Stack. Includes detailed explanation, algorithm, complexity analysis, and clean, interview-ready implementation.
# 1081. Smallest Subsequence of Distinct Characters

![LeetCode](https://img.shields.io/badge/LeetCode-1081-orange)
![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow)
![Language](https://img.shields.io/badge/Language-Java-red)
![Status](https://img.shields.io/badge/Solution-Accepted-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)

## Problem Statement

Given a string `s`, return the **lexicographically smallest subsequence** of `s` that contains every distinct character **exactly once**.

A subsequence is obtained by deleting zero or more characters from the original string without changing the order of the remaining characters.

---

## Examples

### Example 1

**Input**

```text
s = "bcabc"
```

**Output**

```text
abc
```

---

### Example 2

**Input**

```text
s = "cbacdcbc"
```

**Output**

```text
acdb
```

---

## Constraints

- `1 <= s.length <= 1000`
- `s` consists only of lowercase English letters.

---

# Approach

The optimal solution uses a **Greedy Algorithm** combined with a **Monotonic Stack**.

### Key Idea

- Count how many times each character appears.
- Traverse the string.
- Ignore characters already included.
- While:
  - current character is smaller than the last character in the stack
  - the last character appears again later
- Remove the last character to obtain a lexicographically smaller answer.
- Push the current character.

This guarantees:

- Every distinct character appears exactly once.
- The subsequence is lexicographically smallest.

---

# Algorithm

1. Count frequency of every character.
2. Maintain:
   - frequency array
   - visited array
   - stack (StringBuilder)
3. For every character:
   - decrease frequency
   - skip if already used
   - remove larger characters while they appear later
   - add current character
4. Return the stack as the answer.

---

# Java Solution

```java
class Solution {
    public String smallestSubsequence(String text) {
        StringBuilder sb = new StringBuilder();
        int[] count = new int[128];
        boolean[] used = new boolean[128];

        for (char c : text.toCharArray())
            count[c]++;

        for (char c : text.toCharArray()) {
            count[c]--;

            if (used[c])
                continue;

            while (sb.length() > 0 &&
                   sb.charAt(sb.length() - 1) > c &&
                   count[sb.charAt(sb.length() - 1)] > 0) {

                used[sb.charAt(sb.length() - 1)] = false;
                sb.deleteCharAt(sb.length() - 1);
            }

            sb.append(c);
            used[c] = true;
        }

        return sb.toString();
    }
}
```

---

# Dry Run

Input

```text
cbacdcbc
```

Processing

| Character | Stack |
|-----------|-------|
| c | c |
| b | b |
| a | a |
| c | ac |
| d | acd |
| c | acd |
| b | acdb |
| c | acdb |

Output

```text
acdb
```

---

# Complexity Analysis

### Time Complexity

```
O(n)
```

Each character is pushed and popped at most once.

### Space Complexity

```
O(1)
```

Only fixed-size arrays and a stack containing at most 26 lowercase letters are used.

---

# Concepts Used

- Greedy Algorithm
- Monotonic Stack
- String Processing
- Character Frequency
- Lexicographical Ordering

---

# Learning Outcomes

- How greedy decisions lead to optimal solutions.
- Using a monotonic stack for lexicographical optimization.
- Efficient duplicate removal while preserving order.
- Managing character frequency for future occurrence tracking.

---

## Repository Structure

```
.
├── README.md
├── Solution.java
├── CONTRIBUTING.md
├── SECURITY.md
├── LICENSE
└── .gitignore
```

---

## Related Topics

- Stack
- Greedy
- Monotonic Stack
- String
- Hashing

---

## Author

**Ammar Ahmad**

If this repository helped you, consider giving it a ⭐ to support future LeetCode solutions.
