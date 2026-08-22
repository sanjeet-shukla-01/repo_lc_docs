# 1. Find first and last positions of an element in a sorted array
## Using Bounded Binary Search time complexity = O(log n)

```python
def searchRange(nums: list[int], target: int) -> list[int]:
    def findBound(isFirst: bool) -> int:
        left, right = 0, len(nums) - 1
        bound = -1
        
        while left <= right:
            mid = (left + right) // 2
            
            if nums[mid] == target:
                bound = mid
                if isFirst:
                    right = mid - 1  # Keep searching left
                else:
                    left = mid + 1   # Keep searching right
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
                
        return bound

    return [findBound(True), findBound(False)]

# Example Usage:
nums = [5, 7, 7, 8, 8, 10]
target = 8
print(searchRange(nums, target))  # Output: [3, 4]
```


# 2. Search in a rotated sorted array

```python
def search(nums: list[int], target: int) -> int:
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = (left + right) // 2

        if nums[mid] == target:
            return mid

        # Check if the left side is sorted
        if nums[left] <= nums[mid]:
            # Check if target lies within the sorted left side
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # Otherwise, the right side must be sorted
        else:
            # Check if target lies within the sorted right side
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1

    return -1

# Example Usage:
nums = [4, 5, 6, 7, 0, 1, 2]
target = 0
print(search(nums, target))  # Output: 4
```
### Pointes to Remember:
- Determine which half of the array is sorted:
- If nums[left] <= nums[mid], the left half is sorted.
   - Check if target lies within nums[left] and nums[mid]. If yes, narrow the search to the left half (right = mid-1). Otherwise, search the right half (left = mid + 1).

- Else, the right half is sorted.
   - Check if target lies within nums[mid] and nums[right]. If yes, narrow the search to the right half (left = mid + 1). Otherwise, search the left half (right = mid - 1).
