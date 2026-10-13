## Find unique valid email
Example 1:
Input: emails = ["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]
Output: 2
Explanation: "testemail@leetcode.com" and "testemail@lee.tcode.com" actually receive mails.
Example 2:

Input: emails = ["a@leetcode.com","b@leetcode.com","c@leetcode.com"]
Output: 3

- local name and a domain name, separated by the '@' sign. Besides lowercase letters, the email may contain one or more '.' or '+'
- dot is meaning less and that means sam.s and sams are same local name, anything after + is ignored that mean

```python
class Solution(object):
    def numUniqueEmails(self, emails):
        """
        :type emails: List[str]
        :rtype: int
        """
        unique_emails = set()
    
        for email in emails:
            # Split the email into local name and domain name
            local, domain = email.split('@')

            # Ignore everything after the first '+' in the local name
            if '+' in local:
                local = local.split('+')[0]

            # Remove all periods '.' from the local name
            local = local.replace('.', '')

            # Add the normalized email to the set
            unique_emails.add(local + '@' + domain)

        return len(unique_emails)
```

Points to remember
- `local, domain = email.split('@')`
- `local = local.split('+')[0]`
- `local = local.replace('.', '')`
- Use set to store unique emails and return length of set. 


## Problem-2
You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array fruits where fruits[i] is the type of fruit the ith tree produces.

You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:

- You only have two baskets, and each basket can only hold a single type of fruit. There is no limit on the amount of fruit each basket can hold.
- Starting from any tree of your choice, you must pick exactly one fruit from every tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.
- Once you reach a tree with fruit that cannot fit in your baskets, you must stop.

Given the integer array fruits, return the maximum number of fruits you can pick.

 

Example 1:

Input: fruits = [1,2,1]
Output: 3
Explanation: We can pick from all 3 trees.
Example 2:

Input: fruits = [0,1,2,2]
Output: 3
Explanation: We can pick from trees [1,2,2].
If we had started at the first tree, we would only pick from trees [0,1].
Example 3:

Input: fruits = [1,2,3,2,2]
Output: 4
Explanation: We can pick from trees [2,3,2,2].
If we had started at the first tree, we would only pick from trees [1,2].


`This problem can be translated into finding the longest contiguous subarray that contains at most 2 distinct types of integers (fruits). We can solve this efficiently using the Sliding Window technique with a hash map to keep track of the fruit counts in our current window.`
Fruit Into Baskets: Sliding Window
```python
from collections import defaultdict

def totalFruit(fruits: list[int]) -> int:
    count = defaultdict(int)
    left = 0
    max_fruits = 0
    
    for right in range(len(fruits)):
        # 1. EXPAND: Add current fruit to frequency map
        count[fruits[right]] += 1
        
        # 2. SHRINK: If > 2 types, drop elements from the left
        while len(count) > 2:
            count[fruits[left]] -= 1          # Reduce frequency of left-most fruit
            if count[fruits[left]] == 0:
                del count[fruits[left]]       # Completely remove if count hits 0
            left += 1                         # Shift left boundary forward
            
        # 3. RECORD: Track the maximum window size encountered
        max_fruits = max(max_fruits, right - left + 1)
        
    return max_fruits
```

Why import defaultdict, won't python inbluilt dict work?
The Problem with a Regular Dictionary
If you try to add to a fruit count that doesn't exist yet in a regular dictionary, Python will crash with a KeyError.

For example, if your dictionary is completely empty ({}), and you try to do this:

```Python
count = {}
count[1] += 1  # ❌ ERROR! Key '1' doesn't exist yet!
```

To fix this with a regular dictionary, you have to write extra code to check if the key exists before adding to it:

```Python
# Using a regular dict (extra check required):
if fruits[right] not in count:
    count[fruits[right]] = 0
count[fruits[right]] += 1
```

---

## Fibonacci

```python
class Solution(object):
    def fib(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 0:
            return 0
        
        a, b = 0, 1
        for _ in range(2, n + 1):
            a, b = b, a + b
        return b if n > 0 else 0
```

Using recursion

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci_recursive(n):
    if n < 2:
        return n
    return fibonacci_recursive(n - 1) + fibonacci_recursive(n - 2)

```

### Candy Type
Alice has n candies, where the ith candy is of type candyType[i]. Alice noticed that she started to gain weight, so she visited a doctor.
The doctor advised Alice to only eat n / 2 of the candies she has (n is always even). Alice likes her candies very much, and she wants to eat the maximum number of different types of candies while still following the doctor's advice.

Given the integer array candyType of length n, return the maximum number of different types of candies she can eat if she only eats n / 2 of them.

Example 1:
```
Input: candyType = [1,1,2,2,3,3]
Output: 3
Explanation: Alice can only eat 6 / 2 = 3 candies. Since there are only 3 types, she can eat one of each type.
Example 2:
```

```
Input: candyType = [1,1,2,3]
Output: 2
Explanation: Alice can only eat 4 / 2 = 2 candies. Whether she eats types [1,2], [1,3], or [2,3], she still can only eat 2 different types.
```

#### Key Insight
- The maximum number of candies she can eat is len(candyType) // 2.The number of unique candy types available is len(set(candyType)).Therefore, the maximum number of different types she can eat is simply the smaller of these two numbers:If there are more unique types than her allowance ($n / 2$), she can only eat up to her allowance.If there are fewer unique types than her allowance, she can eat all of the unique types available.

```Pyhon
class Solution(object):
    def distributeCandies(self, candyType):
        """
        :type candyType: List[int]
        :rtype: int
        """
        max_allowed = len(candyType) // 2
        unique_types = len(set(candyType))
        
        return min(max_allowed, unique_types)

```



## 1169. Invalid Transactions
A transaction is possibly invalid if:
- the amount exceeds $1000, or;
- if it occurs within (and including) 60 minutes of another transaction with the same name in a different city.
You are given an array of strings transaction where transactions[i] consists of comma-separated values representing the name, time (in minutes), amount, and city of the transaction.

Return a list of transactions that are possibly invalid. You may return the answer in any order.

```Python
    def invalidTransactions(self, transactions):
        """
        :type transactions: List[str]
        :rtype: List[str]
        """
        parsed = []
        for i, t in enumerate(transactions):
            name, time, amount, city = t.split(",")
            parsed.append({
                "index": i,
                "name": name,
                "time": int(time),
                "amount": int(amount),
                "city": city,
                "raw": t
            })
        # print(parsed)

        invalid_indices = set()

        for i in range(len(parsed)):
            # Rule 1: Amount exceeds 1000
            if parsed[i]["amount"] > 1000:
                invalid_indices.add(i)

            # Rule 2: Same name, different city, time difference <= 60 minutes
            for j in range(len(parsed)):
                if i == j:
                    continue

                if (parsed[i]["name"] == parsed[j]["name"] and 
                    parsed[i]["city"] != parsed[j]["city"] and 
                    abs(parsed[i]["time"] - parsed[j]["time"]) <= 60):
                    invalid_indices.add(i)
                    break  # Once it's marked invalid, we can break out of the inner loop

        # Collect all invalid transaction strings using their original indices
        return [transactions[i] for i in sorted(list(invalid_indices))]

```

## 1029. Two City Scheduling
A company is planning to interview 2n people. Given the array costs where costs[i] = [aCosti, bCosti], the cost of flying the ith person to city a is aCosti, and the cost of flying the ith person to city b is bCosti.

Return the minimum cost to fly every person to a city such that exactly n people arrive in each city.

 

Example 1:
```
Input: costs = [[10,20],[30,200],[400,50],[30,20]]
Output: 110
Explanation: 
The first person goes to city A for a cost of 10.
The second person goes to city A for a cost of 30.
The third person goes to city B for a cost of 50.
The fourth person goes to city B for a cost of 20.

The total minimum cost is 10 + 30 + 50 + 20 = 110 to have half the people interviewing in each city.
```

Calculate bCosti - aCosti.
- If this difference is negative, sending them to City B actually saves us money compared to City A.
- If it's positive, sending them to City B costs more.

```Python
def twoCitySchedCost(self, costs):
    """
    :type costs: List[List[int]]
    :rtype: int
    """
    costs.sort(key=lambda x: x[1] - x[0])
    total_cost = 0
    n = len(costs) // 2
    # First n people go to City B (index 1)
    for i in range(n):
        total_cost += costs[i][1]

    # Remaining n people go to City A (index 0)
    for i in range(n, len(costs)):
        total_cost += costs[i][0]

    return total_cost
```
