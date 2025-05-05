# 🧮 Day 23 - Count Inversions

Welcome to Day 23 of the #gfg160 challenge!  
Today’s problem is a classic from the world of sorting and array manipulation: **Count Inversions in an Array**.

---

## 🚀 Problem Statement

Given an array of integers `arr[]`, count the number of **inversions**.

> Two elements `arr[i]` and `arr[j]` form an inversion if `arr[i] > arr[j]` and `i < j`.

- **Inversion Count** gives an idea of how unsorted an array is.
- A **sorted** array has an inversion count of **0**.
- A **reverse sorted** array has the **maximum** inversion count.

---

## 🧠 Approach

We use a **modified Merge Sort** approach for optimal performance.

### Steps:
1. Divide the array recursively using merge sort.
2. While merging, count how many elements in the left half are greater than the right half.
3. Each such case contributes to the inversion count.

### Time Complexity:
- **O(N log N)** — much faster than the naive O(N²)

---

## ✅ Code (Python)

```
class Solution:
    def inversionCount(self, arr):
        def merge_sort(arr):
            if len(arr) <= 1:
                return arr, 0
            mid = len(arr) // 2
            left, inv_left = merge_sort(arr[:mid])
            right, inv_right = merge_sort(arr[mid:])
            merged, inv_split = merge(left, right)
            return merged, inv_left + inv_right + inv_split

        def merge(left, right):
            merged, i, j, inv = [], 0, 0, 0
            while i < len(left) and j < len(right):
                if left[i] <= right[j]:
                    merged.append(left[i])
                    i += 1
                else:
                    merged.append(right[j])
                    inv += len(left) - i
                    j += 1
            merged.extend(left[i:])
            merged.extend(right[j:])
            return merged, inv

        return merge_sort(arr)[1]
```

---
## 💡 Reflection
This problem beautifully combines sorting with counting logic.
Merge Sort not only helps sort arrays efficiently but can also help derive insights like inversion count — perfect example of divide and conquer in action!

---
## 🔖 Tags
#gfg160 #geekstreak2025 #Day23 #DSA #MergeSort #InversionCount #Python #Sorting #ProblemSolving #CodingJourney
