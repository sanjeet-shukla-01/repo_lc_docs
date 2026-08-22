# Find first and last positions of an element in a sorted array
## Using Bounded Binary Search 

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
