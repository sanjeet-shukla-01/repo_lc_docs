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
