# 1. Reverse an Array:
## 1. **Naive Approach:** O(n) Time and O(n) Space

Create a temporary array of same size as the original array. 
Now, copy all elements from original array to the temporary array in reverse order.
Finally, copy all the elements from temporary array back to the original array.

```python
def reverseArray(arr):
    n = len(arr)
    
    # Initialize a Temporary array to store elements in reversed order
    temp = [0] * n
  
    # Copy elements from original array
    # to temp in reverse order
    for i in range(n):
        temp[i] = arr[n - i - 1]
  
    # Copy elements back to original array
    for i in range(n):
        arr[i] = temp[i]

if __name__ == "__main__":
    arr = [1, 4, 3, 2, 6, 5]

    reverseArray(arr)
  
    for i in range(len(arr)):
        print(arr[i], end=" ")
```

### Points to Remember: 
Initializing a list 
- `temp = [0] * n`

Iterating in reverse
- `for i in range(n):
        temp[i] = arr[n - i - 1]`
Iterating in reverse
- `for item in reversed(my_list):
    print(item)`

### 2. Using Two Pointers - O(n) Time and O(1) Space

```python
def reverseArray(arr):
    
    # Initialize left to the beginning 
    # and right to the end
    left = 0
    right = len(arr) - 1
  
    # Iterate till left is less than right
    while left < right:
        
        # Swap the elements at left
        # and right position
        arr[left], arr[right] = arr[right], arr[left]
      
        # Increment the left pointer
        left += 1
      
        # Decrement the right pointer
        right -= 1

if __name__ == "__main__":
    arr = [1, 4, 3, 2, 6, 5]

    reverseArray(arr)
  
    for i in range(len(arr)):
        print(arr[i], end=" ")
```

### Points to Remember: 
In two pointer approach left pointer is initiliazed to zero and right pointer to length-1 
- `eft = 0, right = len(arr) - 1`

Iteration needs a while loop with condition left < right
- `while left < right:`

## 3. Using Single Pointer - O(n) Time and O(1) Space
- Iterate upto n//2
- swap ith and n-i-i th element

```python
def reverseArray(arr):
    n = len(arr)
    
    # Iterate over the first half 
    # and for every index i, swap
    # arr[i] with arr[n - i - 1]
    for i in range(n // 2):
        temp = arr[i]
        arr[i] = arr[n - i - 1]
        arr[n - i - 1] = temp

if __name__ == "__main__":
    arr = [1, 4, 3, 2, 6, 5]

    reverseArray(arr)
  
    for i in range(len(arr)):
        print(arr[i], end=" ")
```

### Points to Remember: 
- Integer division is used to iterate upto `n//2`
- Integer Division `(n//2)` and module division `(n%2)` is used in palindrom number problem


# 2. Maximum and minimum of an array :
## 1. **Naive Approach:** By Sorting the array - O(n log n) Time and O(1) Space

Sort the Array. 
Then take out 0th and -1th element as max and min.
```python
def findMinMax(arr):
    
    # Sort array
    sorted_arr = sorted(arr)
    return [sorted_arr[0], sorted_arr[-1]] 

if __name__ == "__main__":
    arr = [3, 5, 4, 1, 9]
    result = findMinMax(arr)
    print("%d %d" % (result[0], result[1]))
```

### Points to Remember: 
- To sort an array `sorted()` function is used
- In order to take lastelement of an array use arr[-1]


## 2. **Better Approach:** Iterating the array - O(n) Time and O(1) Space

```python
def findMinMax(arr):
    mini = float('inf') 
    maxi = float('-inf')
    
    # Find minimum and maximum
    for num in arr: 
        if num < mini:
            mini = num
        if num > maxi:
            maxi = num
    
    return [mini, maxi]

if __name__ == "__main__":
    arr = [3, 5, 4, 1, 9]
    result = findMinMax(arr)
    print(result[0], result[1])
```
### Points to Remember: 
- To find min and max we can start by defining `+infinity` and `-infinity` as `float('inf')` and `float('-inf')`


## 3. Optimal Approach: Comparing in pairs - O(n) Time and O(1) Space
This approach finds the smallest and largest numbers in a list by reducing the number of comparisons. If the list has an odd number of elements, it initializes both the minimum and maximum with the first element. If it has an even number, it compares the first two elements to set the initial min and max. 

It then processes the remaining elements in pairs. For each pair, it identifies the smaller and larger number, then updates the current minimum and maximum accordingly. After all pairs are checked, the final minimum and maximum values are returned.

```python
def find_min_max(arr):
    n = len(arr)

    # Initialize min and max
    if n % 2 == 1:
        mini = maxi = arr[0]
        i = 1
    else:
        if arr[0] < arr[1]:
            mini = arr[0]
            maxi = arr[1]
        else:
            mini = arr[1]
            maxi = arr[0]
        i = 2

    # Process elements in pairs
    while i < n - 1:
        if arr[i] < arr[i + 1]:
            mini = min(mini, arr[i])
            maxi = max(maxi, arr[i + 1])
        else:
            mini = min(mini, arr[i + 1])
            maxi = max(maxi, arr[i])
        i += 2

    return [mini, maxi]

def main():
    arr = [3, 5, 4, 1, 9]
    result = find_min_max(arr)
    print(result[0], result[1])

if __name__ == "__main__":
    main()
```

# 3. Kth Smallest
Given an integer array arr[] and an integer k, find and return the kth smallest element in the given array.
> Note: The kth smallest element is determined based on the sorted order of the array.

## 1. Naive Approach: Using sort
```python
def kth_smallest_sort(arr, k):
    # Sort the array in ascending order
    arr.sort()
    # k-th smallest element is at index k-1
    return arr[k - 1]
```
### Points to Remember: 
- `arr.sort()` does inplace modification, while `sorted(arr)` creates new list. 

## 2. This approach uses a heap under the hood

```python
import heapq

def findKthSmallest(nums, k):
    # Python's heapq is a min-heap by default.
    # We negate numbers to simulate a Max-Heap!
    max_heap = []
    
    for num in nums:
        # Push negated value into the heap
        heapq.heappush(max_heap, -num)
        
        # If heap size exceeds k, drop the largest element (which is the smallest negative)
        if len(max_heap) > k:
            heapq.heappop(max_heap)
            
    # The top element is negated, so convert it back
    return -max_heap[0]

# Example Usage:
nums = [7, 10, 4, 3, 20, 15]
k = 3
print(f"The {k}rd smallest element is:", findKthSmallest(nums, k))
# Output: 7 (Sorted array: [3, 4, 7, 10, 15, 20])
```

### Points to Remember
- One Liner: `k_smallest = heapq.nsmallest(k, input_list)`
- Max Heap, Min Heap

# 4. Given an array arr[] containing only 0s, 1s, and 2s. Sort the array in ascending order.
> Note: You need to solve this problem without utilizing the built-in sort function.

This is the classic Dutch National Flag Problem, famously posed by Edsger Dijkstra.

Since the array only contains 0s, 1s, and 2s, the optimal solution is the 3-Way Partitioning (Two-Pointer / Three-Pointer) approach, which sorts the array in a single pass without using extra memory.

💡 The Core Intuition
We divide the array into three sections using three pointers:
- low: Boundary for 0s (everything before low is 0).
- mid: Current element being evaluated.
- high: Boundary for 2s (everything after high is 2).

As we traverse with mid:
- If arr[mid] == 0: Swap with arr[low], increment both low and mid.
- If arr[mid] == 1: It's already in the correct relative zone! Just increment mid.
- If arr[mid] == 2: Swap with arr[high], decrement high (do not increment mid yet, because the swapped element from high still needs to be checked).

```python
def sort012(arr):
    low = 0
    mid = 0
    high = len(arr) - 1
    
    while mid <= high:
        if arr[mid] == 0:
            arr[low], arr[mid] = arr[mid], arr[low]
            low += 1
            mid += 1
        elif arr[mid] == 1:
            mid += 1
        else:  # arr[mid] == 2
            arr[mid], arr[high] = arr[high], arr[mid]
            high -= 1

# Example Usage:
arr = [2, 0, 2, 1, 1, 0]
sort012(arr)
print("Sorted array:", arr)
# Output: [0, 0, 1, 1, 2, 2]
```


# 5. Find Union and Intersection of Sorted Array

## Naive Approach
```python
# Initial sample arrays (lists)
array1 = [1, 2, 2, 3, 4]
array2 = [3, 4, 4, 5, 6]

# Convert to sets to eliminate duplicates
set1 = set(array1)
set2 = set(array2)

# --- UNION ---
# Combines all unique elements from both arrays
union_result = list(set1 | set2)  # Or use: set1.union(set2)
print("Union:", union_result)  
# Output: [1, 2, 3, 4, 5, 6]

# --- INTERSECTION ---
# Keeps only the elements present in both arrays
intersection_result = list(set1 & set2)  # Or use: set1.intersection(set2)
print("Intersection:", intersection_result)  
# Output: [3, 4]
```

## Better Appraoch without using any inbuilt data strucuture
```python
def find_union_and_intersection(arr1, arr2):
    n, m = len(arr1), len(arr2)
    
    # --- 1. UNION ---
    union = []
    i, j = 0, 0
    while i < n and j < m:
        # Pick the smaller element to maintain sorted order
        if arr1[i] < arr2[j]:
            val = arr1[i]
            i += 1
        elif arr2[j] < arr1[i]:
            val = arr2[j]
            j += 1
        else:  # arr1[i] == arr2[j]
            val = arr1[i]
            i += 1
            j += 1
            
        # Avoid duplicate elements in the result
        if not union or union[-1] != val:
            union.append(val)
            
    # Process remaining elements in arr1
    while i < n:
        if not union or union[-1] != arr1[i]:
            union.append(arr1[i])
        i += 1
        
    # Process remaining elements in arr2
    while j < m:
        if not union or union[-1] != arr2[j]:
            union.append(arr2[j])
        j += 1

    # --- 2. INTERSECTION ---
    intersection = []
    i, j = 0, 0
    while i < n and j < m:
        if arr1[i] < arr2[j]:
            i += 1
        elif arr2[j] < arr1[i]:
            j += 1
        else:  # Equal elements -> common element
            if not intersection or intersection[-1] != arr1[i]:
                intersection.append(arr1[i])
            i += 1
            j += 1

    return union, intersection


# Example Usage:
arr1 = [1, 2, 2, 3, 4, 7]
arr2 = [2, 3, 5, 7, 8]

union_res, inter_res = find_union_and_intersection(arr1, arr2)

print("Union:", union_res)         # Output: [1, 2, 3, 4, 5, 7, 8]
print("Intersection:", inter_res)  # Output: [2, 3, 7]
```



### Points to Remeber
- How while loop is used for two pointers `while i < n and j < m:`
- To check whether result array is empty or result array already contains current elelment `if not union or union[-1] != arr1[i]:`
- `arr1[i] < arr2[j]`: Move i forward (the smaller value cannot match any future larger items in arr2).
- `arr1[i] > arr2[j]`: Move j forward.
- `arr1[i] == arr2[j]`: Move both pointers forward (i++, j++).



# 6 Cyclically Rotate an Array by 1




# 7 Move all negative numbers to beginning and positive to end with
## 1. Using arr.sort
```python
def move(arr):
    arr.sort()
    return arr
```



### Points to Remeber
- 
