
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
    if len(arr) > 1:
        mid = len(arr) // 2
        
        left = arr[:mid]
        right = arr[mid:]
        
        # Recursively sort both halves
        merge_sort(left)
        merge_sort(right)
        
        i = j = k = 0
        
        # Merge the sorted halves
        while i < len(left) and j < len(right):
            if left[i] < right[j]:
                arr[k] = left[i]
                i += 1
            else:
                arr[k] = right[j]
                j += 1
            k += 1
        
        # Remaining elements
        while i < len(left):
            arr[k] = left[i]
            i += 1
            k += 1
        
        while j < len(right):
            arr[k] = right[j]
            j += 1
            k += 1
    
    return arr

# Example
arr = [38, 27, 43, 3, 9, 82, 10]
print(merge_sort(arr))
```

### Output:
```
[3, 9, 10, 27, 38, 43, 82]
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
    
    pivot = arr[0]  # choosing first element as pivot
    left = []
    right = []
    
    for i in arr[1:]:
        if i <= pivot:
            left.append(i)
        else:
            right.append(i)
    
    return quick_sort(left) + [pivot] + quick_sort(right)

# Example
arr = [10, 7, 8, 9, 1, 5]
print(quick_sort(arr))
```

### Output:
```
[1, 5, 7, 8, 9, 10]
```

### 🔹 Complexity:

* Best: O(n log n)
* Worst: O(n²)
* Space: O(log n)



# 🔸 6. Heap Sort

### 🔹 Idea:

- Heap Sort uses a Binary Heap (Max Heap) to sort elements.
- First build a heap, then repeatedly extract the maximum element.

### 🔹 Code:

```python
def heapify(arr, n, i):
    largest = i
    left = 2*i + 1
    right = 2*i + 2

    # Check left child
    if left < n and arr[left] > arr[largest]:
        largest = left

    # Check right child
    if right < n and arr[right] > arr[largest]:
        largest = right

    # Swap and continue heapifying
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)


def heap_sort(arr):
    n = len(arr)

    # Build max heap
    for i in range(n//2 - 1, -1, -1):
        heapify(arr, n, i)

    # Extract elements
    for i in range(n-1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]  # swap
        heapify(arr, i, 0)

    return arr


# Example
arr = [12, 11, 13, 5, 6, 7]
print(heap_sort(arr))
```

### Output:
```
[5, 6, 7, 11, 12, 13]
```

### 🔹 Complexity:

* Time: O(n log n)
* Space: O(1)



# 🔸 7. Counting Sort (Non-Comparison)

### 🔹 Idea:

- Counting Sort is a non-comparison sorting algorithm that counts the occurrences of each element.

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
    
    # Create count array
    count = [0] * (max_val + 1)
    
    # Count occurrences
    for num in arr:
        count[num] += 1
    
    # Build sorted array
    sorted_arr = []
    for i in range(len(count)):
        sorted_arr.extend([i] * count[i])
    
    return sorted_arr


# Example
arr = [4, 2, 2, 8, 3, 3, 1]
print(counting_sort(arr))
```

### Output:
```
[1, 2, 2, 3, 3, 4, 8]
```

### 🔹 Complexity:

* Time: O(n + k)
* Space: O(k)



# 🔸 8. Radix Sort

## 🔹 Idea:

- Radix Sort is a non-comparison sorting algorithm that sorts numbers digit by digit (from least significant digit to most significant digit).
- 
## 🔹 Radix Sort Example:

👉 Input:
```
[170, 45, 75, 90, 802, 24, 2, 66]
```
### 🔸 Step 1: Sort by **Units Place (1s digit)**
```
Digits → [0, 5, 5, 0, 2, 4, 2, 6]

Buckets:
0 → [170, 90]
2 → [802, 2]
4 → [24]
5 → [45, 75]
6 → [66]

Result → [170, 90, 802, 2, 24, 45, 75, 66]
```
### 🔸 Step 2: Sort by **Tens Place (10s digit)**
```
Digits → [7, 9, 0, 0, 2, 4, 7, 6]

Buckets:
0 → [802, 2]
2 → [24]
4 → [45]
6 → [66]
7 → [170, 75]
9 → [90]

Result → [802, 2, 24, 45, 66, 170, 75, 90]
```
### 🔸 Step 3: Sort by **Hundreds Place (100s digit)**

```
Digits → [8, 0, 0, 0, 0, 1, 0, 0]

Buckets:
0 → [2, 24, 45, 66, 75, 90]
1 → [170]
8 → [802]

Result → [2, 24, 45, 66, 75, 90, 170, 802]
```

## 🔥 Final Sorted Output
```
[2, 24, 45, 66, 75, 90, 170, 802]
```

## 🔹 Quick Pattern 🧠

👉 **Units → Tens → Hundreds → Final Sorted**

## 🔹 Code:

```python
def counting_sort(arr, exp):
    n = len(arr)
    output = [0] * n
    count = [0] * 10  # digits 0-9

    # Count occurrences of digits
    for i in range(n):
        index = (arr[i] // exp) % 10
        count[index] += 1

    # Update count[i] so it contains actual position
    for i in range(1, 10):
        count[i] += count[i - 1]

    # Build output array (stable sort)
    for i in range(n - 1, -1, -1):
        index = (arr[i] // exp) % 10
        output[count[index] - 1] = arr[i]
        count[index] -= 1

    # Copy to original array
    for i in range(n):
        arr[i] = output[i]


def radix_sort(arr):
    max_val = max(arr)
    exp = 1

    # Apply counting sort for every digit
    while max_val // exp > 0:
        counting_sort(arr, exp)
        exp *= 10

    return arr


# Example
arr = [170, 45, 75, 90, 802, 24, 2, 66]
print(radix_sort(arr))
```

### Output:
```
[2, 24, 45, 66, 75, 90, 170, 802]
```

### 🔹 Complexity:

* Time: O(nk)
* Space: O(n)



# 🔸 9. Bucket Sort

### 🔹 Idea:

- Bucket Sort distributes elements into different buckets, sorts each bucket, and then combines them.

### 🔹 Code:

```python
def bucket_sort(arr):
    if len(arr) == 0:
        return arr

    # Create buckets
    bucket_count = len(arr)
    buckets = [[] for _ in range(bucket_count)]

    # Put elements into buckets
    max_val = max(arr)
    for num in arr:
        index = int(num * bucket_count / (max_val + 1))
        buckets[index].append(num)

    # Sort each bucket
    for bucket in buckets:
        bucket.sort()

    # Merge buckets
    sorted_arr = []
    for bucket in buckets:
        sorted_arr.extend(bucket)

    return sorted_arr


# Example
arr = [0.42, 0.32, 0.23, 0.52, 0.25, 0.47]
print(bucket_sort(arr))
```

### Output:
```
[0.23, 0.25, 0.32, 0.42, 0.47, 0.52]
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


