### What is difference between `sorted()` vs arr.sort() methods?
- sorted() leaves original object unchanged
- sorted is built in function that takes Any iterable (list, tuple, string, set, dict)
- Returns a brand new sorted list, hence take memory 
---
- arr.sort() is a list method that only works on lists
- arr.sort() is Efficient, does inplace modification to existing list
- arr.sort() returns None


### How to sort an Array in Descending Order
- 1. using `arr.sort(reverse=True)`
  ```python
  numbers = [23, 4, 89, 12, 56]
  numbers.sort(reverse=True)
  ```
- 2. using `sorted(arr, reverse=True)`
  ```python
  numbers = [23, 4, 89, 12, 56]
  sorted_numbers = sorted(numbers, reverse=True)
  ```

### What is min heap and max heap?
- **Min Heap** In a Min Heap, the value of each parent node is less than or equal to its child nodes.
- Key Feature: The absolute smallest element is always at the root.
- Use Case: Perfect for finding or extracting the minimum element instantly (e.g., in priority queues or Dijkstra's algorithm).
---
- **Max Heap** In a Max Heap, the value of each parent node is greater than or equal to its child nodes.
- Key Feature: The absolute largest element is always at the root.
- Use Case: Perfect for applications like gaming leaderboards or Heap Sort where you need constant O(1) access to the highest number.

**Common Characteristics** Both heaps share the following core traits:
- Complete Binary Tree: Every level of the tree is fully filled, except possibly the last level, which is filled from left to right.
- Array Representation: They are efficiently stored in arrays without using pointers.
- For a node at index i, its children are located at indices 2i+1 and 2i+2, and its parent at \(\frac{i-1}{2}\).
- Efficiency: Peeking at the maximum or minimum takes O(1) time, while inserting or removing elements takes \(O(\log N)\) time.
- For an easy visual breakdown of how the parent-child relationships change between these two structures
  <img width="1193" height="569" alt="image" src="https://github.com/user-attachments/assets/5ee7437f-ba7d-4e1c-843c-e6b20fea66bc" />

