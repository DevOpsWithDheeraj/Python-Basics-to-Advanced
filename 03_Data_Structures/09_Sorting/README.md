
# 🔹 What is Sorting?

- **Sorting** is the process of arranging elements in a collection based on a comparison operator.

👉 Example: 
- Unsorted → `[5, 2, 9, 1]` <br>
- Sorted (Ascending) → `[1, 2, 5, 9]`


## 🔹 Why is Sorting Important?

* Faster searching (Binary Search requires sorted data)
* Data organization
* Duplicate detection
* Efficient algorithms (e.g., merging, grouping)



## 🔹 Types of Sorting Algorithms

Sorting algorithms are mainly classified into:

### 1. **Comparison-Based Sorting**

* Compare elements to decide order
* Examples:

  * Bubble Sort
  * Selection Sort
  * Insertion Sort
  * Merge Sort
  * Quick Sort
  * Heap Sort

### 2. **Non-Comparison-Based Sorting**

* Do not compare elements directly
* Examples:

  * Counting Sort
  * Radix Sort
  * Bucket Sort



# 🔸 1. Bubble Sort

### 🔹 Idea:

Repeatedly swap adjacent elements if they are in the wrong order.

### 🔹 Example:

```
[5, 2, 9, 1]

Pass 1:
[2, 5, 1, 9]
Pass 2:
[2, 1, 5, 9]
Pass 3:
[1, 2, 5, 9]
```

### 🔹 Python Code:

```python
def bubble_sort(arr):
    n = len(arr)
    
    for i in range(n):
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                # swap
                arr[j], arr[j+1] = arr[j+1], arr[j]
    
    return arr

# Example
arr = [64, 34, 25, 12, 22, 11, 90]
print(bubble_sort(arr))
```

### Output:
```
[11, 12, 22, 25, 34, 64, 90]
```

### 🔹 Complexity:

* Time: O(n²)
* Space: O(1)



# 🔸 2. Selection Sort

### 🔹 Idea:

Find the minimum element and place it at the beginning.

### 🔹 Example:

```
[5, 2, 9, 1]

Step 1: 1 → swap with 5 → [1, 2, 9, 5]
Step 2: 2 is already correct
Step 3: 5 → swap with 9 → [1, 2, 5, 9]
```

### 🔹 Code:

```python
def selection_sort(arr):
    n = len(arr)
    
    for i in range(n):
        min_index = i
        
        for j in range(i+1, n):
            if arr[j] < arr[min_index]:
                min_index = j
        
        # swap
        arr[i], arr[min_index] = arr[min_index], arr[i]
    
    return arr

# Example
arr = [64, 25, 12, 22, 11]
print(selection_sort(arr))
```

### Output:
```
[11, 12, 22, 25, 64]
```

### 🔹 Complexity:

* Time: O(n²)
* Space: O(1)



# 🔸 3. Insertion Sort

### 🔹 Idea:

Insert each element into its correct position in a sorted portion.

### 🔹 Example:

```
[5, 2, 9, 1]

Step 1: [5]
Step 2: [2, 5]
Step 3: [2, 5, 9]
Step 4: [1, 2, 5, 9]
```

### 🔹 Code:

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        
        # Move elements greater than key
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        
        arr[j + 1] = key
    
    return arr

# Example
arr = [12, 11, 13, 5, 6]
print(insertion_sort(arr))
```

### Output:
```
[5, 6, 11, 12, 13]
```

### 🔹 Complexity:

* Time: O(n²), Best: O(n)
* Space: O(1)



# 🔸 4. Merge Sort (Divide & Conquer)

### 🔹 Idea:

Divide array → sort halves → merge them.

### 🔹 Example:

```
[5, 2, 9, 1]
→ [5, 2] & [9, 1]
→ [2, 5] & [1, 9]
→ [1, 2, 5, 9]
```

### 🔹 Code:

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr)//2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    result = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

### 🔹 Complexity:

* Time: O(n log n)
* Space: O(n)



# 🔸 5. Quick Sort

### 🔹 Idea:

Pick a pivot → partition → sort recursively.

### 🔹 Example:

```
[5, 2, 9, 1]
Pivot = 5

Left: [2, 1]
Right: [9]

→ [1, 2, 5, 9]
```

### 🔹 Code:

```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[0]
    left = [x for x in arr[1:] if x <= pivot]
    right = [x for x in arr[1:] if x > pivot]

    return quick_sort(left) + [pivot] + quick_sort(right)
```

### 🔹 Complexity:

* Best: O(n log n)
* Worst: O(n²)
* Space: O(log n)



# 🔸 6. Heap Sort

### 🔹 Idea:

Use a **heap data structure** (max heap).

### 🔹 Code:

```python
import heapq

def heap_sort(arr):
    heapq.heapify(arr)
    return [heapq.heappop(arr) for _ in range(len(arr))]
```

### 🔹 Complexity:

* Time: O(n log n)
* Space: O(1)



# 🔸 7. Counting Sort (Non-Comparison)

### 🔹 Idea:

Count occurrences of elements.

### 🔹 Example:

```
[4, 2, 2, 1]
Count → [1:1, 2:2, 4:1]
Result → [1, 2, 2, 4]
```

### 🔹 Code:

```python
def counting_sort(arr):
    max_val = max(arr)
    count = [0] * (max_val + 1)

    for num in arr:
        count[num] += 1

    result = []
    for i in range(len(count)):
        result.extend([i] * count[i])

    return result
```

### 🔹 Complexity:

* Time: O(n + k)
* Space: O(k)



# 🔸 8. Radix Sort

### 🔹 Idea:

Sort numbers digit by digit.

### 🔹 Code:

```python
def radix_sort(arr):
    exp = 1
    max_val = max(arr)

    while max_val // exp > 0:
        buckets = [[] for _ in range(10)]

        for num in arr:
            buckets[(num // exp) % 10].append(num)

        arr = []
        for bucket in buckets:
            arr.extend(bucket)

        exp *= 10

    return arr
```

### 🔹 Complexity:

* Time: O(nk)
* Space: O(n)



# 🔸 9. Bucket Sort

### 🔹 Idea:

Distribute elements into buckets and sort individually.

### 🔹 Code:

```python
def bucket_sort(arr):
    bucket = [[] for _ in range(len(arr))]

    for num in arr:
        index = int(num * len(arr))
        bucket[index].append(num)

    for b in bucket:
        b.sort()

    result = []
    for b in bucket:
        result.extend(b)

    return result
```

### 🔹 Complexity:

* Average: O(n + k)
* Worst: O(n²)



# 🔹 Comparison Table

| Algorithm      | Time Complexity | Space    | Stable |
| -------------- | --------------- | -------- | ------ |
| Bubble Sort    | O(n²)           | O(1)     | Yes    |
| Selection Sort | O(n²)           | O(1)     | No     |
| Insertion Sort | O(n²)           | O(1)     | Yes    |
| Merge Sort     | O(n log n)      | O(n)     | Yes    |
| Quick Sort     | O(n log n)      | O(log n) | No     |
| Heap Sort      | O(n log n)      | O(1)     | No     |
| Counting Sort  | O(n+k)          | O(k)     | Yes    |
| Radix Sort     | O(nk)           | O(n)     | Yes    |
| Bucket Sort    | O(n+k)          | O(n)     | Yes    |



# 🔹 Important Points

* **Stable Sort:** Maintains order of equal elements
* **In-place Sort:** Uses constant memory
* **Divide & Conquer:** Merge, Quick
* **Best General Use:** Quick Sort / Merge Sort
* **For Integers:** Counting / Radix


