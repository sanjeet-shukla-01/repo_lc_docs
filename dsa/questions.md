### What is difference between `sorted()` vs arr.sort() methods?
- sorted() leaves original object unchanged
- sorted is built in function that takes Any iterable (list, tuple, string, set, dict)
- Returns a brand new sorted list, hence take memory 

- arr.sort() is a list method that only works on lists
- Efficient, does inplace modification to existing list
- returns None
