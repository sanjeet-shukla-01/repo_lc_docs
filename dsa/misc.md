def findNumber(arr, k):
    # Write your code here
    for element in arr:
        if element == k:
            return "YES"
    return "NO"



Fizz Buzz
def fizzBuzz(n):
    for i in range(1, n+1):
        if i % 15 == 0:
            print("FizzBuzz")
        elif i % 3 == 0:
            print("Fizz")
        elif i % 5 == 0:
            print("Buzz")
        else: 
            print(i)
