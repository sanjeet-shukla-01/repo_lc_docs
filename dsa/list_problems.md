# Reverse an Array:
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
