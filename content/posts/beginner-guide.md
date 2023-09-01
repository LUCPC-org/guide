+++
title = "Beginner's Guide"
author = "Cameron Kauffman"
date = 2023-09-01T13:42:01-04:00
katex = true
+++

This guide is aimed towards students that may be new to programming or competitive programming. Many of the topics covered in this guide are not specific to competitive programming, but are still important to know.

# Table of Contents

- [What is the ICPC?](#what-is-the-icpc)
- [This seems hard, am I even good enough to compete?](#this-seems-hard-am-i-even-good-enough-to-compete)
- [How do I practice?](#how-do-i-practice)
- [What is Leetcode and Kattis?](#what-is-leetcode-and-kattis)
- [How do I get started?](#how-do-i-get-started)
  - [Missing Number Problem](#missing-number-problem)
    - [Solution 1](#solution-1)
    - [Solution 2](#solution-2)
- [The most important data structure in Competitive Programming](#the-most-important-data-structure-in-competitive-programming)
    - [Let's look at a map](#lets-look-at-a-map)
        - [What is `std::`?](#what-is-std)
    - [Why are maps so important?](#why-are-maps-so-important)
    - [Where can this be used?](#where-can-this-be-used)
    - [Contains Duplicate Problem](#contains-duplicate-problem)
    - [Two Sum Problem](#two-sum-problem)

## What is the ICPC?

The ICPC is the International Collegiate Programming Contest. It is a programming competition where teams of three students compete to solve as many problems as they can in five hours. The problems are algorithmic in nature and require a good understanding of data structures and algorithms. The ICPC is a great way to learn how to solve programming problems and to meet other students interested in programming.

In the United States, we have 2 competitions to go through until we can go to the World Finals for the ICPC. First, we have the regional competition, where Liberty competes in the Mid-Atlantic Regional. Second, there is a national competition hosted at UCF (University of Central Florida), where, if your team performs well enough, you can attend the World Finals, which is hosted at a different place each year.

## This seems hard; am I even good enough to compete?

Yes! The ICPC is a great way to learn how to solve programming problems. You don't need to be an expert to compete. In fact, most students that compete are not experts. There are a ton of ways to learn how to solve programming problems. The best way is to just practice.

## How do I practice?

The best way to practice is to just do problems. The two websites we mainly use to solve problems on are [leetcode.com](https://leetcode.com) and [open.kattis.com](https://open.kattis.com).

## What are Leetcode and Kattis?

Leetcode and Kattis are two websites that host programming problems. Leetcode is more geared towards interview questions, while Kattis is more geared towards competitive programming. Both websites are great resources for learning how to solve programming problems.

At the ICPC, we use Kattis to track our submissions to problems.

## How do I get started?

Awesome question! How about we do a programming problem? Let's do a very simple one called the [Missing Number Problem](https://leetcode.com/problems/missing-number/)

### Missing Number Problem

[Link on Leetcode](https://leetcode.com/problems/missing-number/)

The problem description says:

> Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return *the only number in the range that is missing from the array*.

So, from this description we can see that there are going to be `n` numbers in the array and that the numbers are going to be in the range `[0, n]`. We also know that there is going to be one number missing from the array, and we need to find that number and return it.

Well, there are multiple ways to solve this problem. Let's think of a really simple one first.

#### Solution 1

My first thought when I saw this problem was to sort the array. The reason I thought this was because if we sort the array then every number is greater than the number before it, much like a number line or a **range**. Because, the numbers are in the range `[0, n]`, we can use this to our advantage.

When we sort the array, every element (number) **should** correspond to the current position in the array. 

If the array was `[0, 1, 2, 3]`, then the number `0` would be at index `0`, the number `1` would be at index `1`, and so on. **But**, we know that there is a missing number, so now all we have to do is compare each number with the index it is at. Whichever number does not equal its index is the missing number.

Let's try it out.

```python
def missingNumber(self, nums: list[int]) -> int:
    nums.sort() # Sort the array

    # Loop through every element in the array and check 
    # if the index is equal to the number
    for i in range(len(nums)):
        if i != nums[i]:
            return i # If it isn't, then return the index
```
```cpp
int missingNumber(vector<int>& nums) {
    sort(nums.begin(), nums.end()); // Sort the array

    // Loop through every element in the array and check 
    // if the index is equal to the number
    for (int i = 0; i < nums.size(); i++) {
        if (i != nums[i]) {
            return i; // If it isn't, then return the index
        }
    }
}
```

**Awesome!** This is a great way to think through the problem. We sorted the array and now because every element is **unique** and in the range `[0, n]` we can just compare the number to the index. If the number is not equal to the index, then we know that the index is the number that is missing.

**But wait!** This doesn't solve the problem all the time. What would happen if the array was `[0, 1, 2]`? 

Well our algorithm will not find any number that is missing, because every number is equal to its index. But we know that every time there **is** a missing number, so in this case the missing number has to be **3**. How can we fix our algorithm to include this logic?

This is how I have done it:

```python
def missingNumber(self, nums: list[int]) -> int:
    nums.sort() # Sort the array

    # Loop through every element in the array and check 
    # if the index is equal to the number
    for i in range(len(nums)):
        if i != nums[i]:
            return i # If it isn't, then return the index
    
    return len(nums)
```
```cpp
int missingNumber(vector<int>& nums) {
    sort(nums.begin(), nums.end()); // Sort the array

    // Loop through every element in the array and check 
    // if the index is equal to the number
    for (int i = 0; i < nums.size(); i++) {
        if (i != nums[i]) {
            return i; // If it isn't, then return the index
        }
    }

    
    return nums.size();
}
```

As you can see, all I am doing at the end is returning the size of the array at the end. This is because if we get to the end of the array, then we know that the missing number is the last number in the range `[0, n]` -- which we can deduct is the size of the array.

So, now, you've just come up with one solution to the problem, but there are many other ways to solve it. Let's look at another way.

#### Solution 2

One idea we can grab from the problem description is, "What if we could calculate the sum of the range of numbers, `[0, n]`, and then compare that to the sum of `nums`?" Using this, you could find the missing number pretty fast, and you wouldn't have to sort the array.

Well, it turns out some very smart mathematicians have already figured out how to calculate the sum of `[0, n]`.

The formula is the following, where \\(n\\) is the number of elements in the array:

$$\frac{n(n+1)}{2}$$

So, let's try it out in code!

```py
def missingNumber(self, nums: list[int]) -> int:
    n = len(nums) # Get the length of the array

    # Calculate the sum of [0, n]
    sum = (n * (n + 1)) // 2

    # Loop through every element in the array and subtract it from the sum
    for num in nums:
        sum -= num

    return sum # Return the sum
```
```cpp
int missingNumber(vector<int>& nums) {
    int n = nums.size(); // Get the length of the array

    // Calculate the sum of [0, n]
    int sum = (n * (n + 1)) / 2;

    // Loop through every element in the array and subtract it from the sum
    for (int num : nums) {
        sum -= num;
    }

    return sum; // Return the sum
}
```

Okay, one thing to note is that in the Python solution I used two slashes when dividing.
```py
sum = (n * (n + 1)) // 2
```

The reason I do this is because two slashes in Python means to do **integer division**. This means when I divide two numbers, the result will be rounded down. So if I divide `5` by `2`, I will get `2`. This is because `2` is the closest integer to `2.5` that is less than `2.5`.

C++ automatically does this for us because the type of `sum` is `int`. So, we don't have to worry about it.

Our solution collects the sum of `[0, n]` and then loops through the array and subtracts every element from the sum. This will leave us with the missing number.

There are so many ways to solve this problem, and these are just two of them. I encourage you to try and come up with your own solutions. You can also look at other people's solutions on Leetcode to see how they solved it.

## The most important data structure in Competitive Programming

Other than arrays (which are not considered data structures), there exists one single data structure that is arguably the most important data structure in competitive programming. This data structure called a **map**.

A map is a data structure that maps a single **key** to a **value**. In Python, a map is called a dictionary. In C++, a map is called an `unordered_map`.

> We will not be talking about ordered maps because they are not as important as unordered maps.

### Let's look at a map

Okay so a map *maps* a key to a value. What does that mean? Well, let's look at an example.

```py
# Create a map
ages = {}

ages['Cameron'] = 19
ages['Dondi'] = 59

print(ages['Cameron'])
print(ages['Dondi'])
```

In this piece of code I created a map, `ages = {}`, and added some **key-value** pairs to it. The two **keys** I added were the strings, `'Cameron'` and `'Dondi'`. The two **values** I added were the numbers, `19` and `59`.

When I print out, `print(ages['Cameron'])`, it is going to print `19`, because the map knows that `'Cameron'` is *mapped* to `19`. The same can be said for `print(ages['Dondi'])`.

What would happen if I did this:
```py
# Create a map
ages = {}

ages['Cameron'] = 19
ages['Dondi'] = 59

ages['Cameron'] = 17

print(ages['Cameron'])
print(ages['Dondi'])
```

Well, the output would be `17` and `59`. This is because when I set `ages['Cameron'] = 17`, I am telling the map to change the value of `'Cameron'` to `17`. So, when I print out `ages['Cameron']`, it is going to print `17`.

This is **important** to remember that a map can only have **unique** keys in it. When I set `ages['Cameron'] = 17`, I am not adding a new key-value pair to the map, I am just changing the value of the key `'Cameron'`.

Here is an example of the same program in **C++**:

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main() {
    // Create a map
    std::unordered_map<std::string, int> ages;

    ages["Cameron"] = 19;
    ages["Dondi"] = 59;

    ages["Cameron"] = 17;

    std::cout << ages["Cameron"] << std::endl;
    std::cout << ages["Dondi"] << std::endl;
}
```

#### What is `std::`?

One quick thing we can do to make our C++ code look a little cleaner is to make sure we don't have to add the `std::` prefix on everything. The reason we have to initially do this is because, even though we included the **libraries** using `#include`, C++ still wants us to tell it where the functions are coming from. 

So, by adding `using namespace std;` at the top of our program, we can tell C++ that we want to use the `std` namespace for all of our functions.

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

using namespace std;

int main() {
    // Create a map
    unordered_map<string, int> ages;

    ages["Cameron"] = 19;
    ages["Dondi"] = 59;

    ages["Cameron"] = 17;

    cout << ages["Cameron"] << endl;
    cout << ages["Dondi"] << endl;
}
```

Now our code looks much neater! Most of the time this will already be done for you in leetcode behind the scenes, but when you are using Kattis, you will have to do this yourself.

### Why are maps so important?

Maps are so important because they allow us to store data in a way that is easy to access. What we call an unordered map can also be called a **Hash Map**. This is because the way a map works is by using a **hash function** to map a key to a value.

A hash function is a function that takes in a key and returns a value. The value that is returned is the index of the key in the map. This is why maps are so fast. They are able to find the index of a key in constant time, \\(O(1)\\), which is the fastest time possible.

You don't need to know how hash functions work, but it is important to remember that they are fast and no matter how big the map is, it will always be able to find the index of a key in constant time.

### Where can this be used?

So this would be useful for storing a database of people and their ages, but how can this be used in competitive programming?

I'm so glad you asked! 

*Why am I talking to myself??*

We're going to fully understand how a map can be applied to two leetcode problems.

### Contains Duplicate Problem

[Link on Leetcode](https://leetcode.com/problems/contains-duplicate/)

> Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

Okay, so this problem is asking us to find out if there are any duplicate numbers in the array. 

How can we implement a map to help us solve this problem?

The first thing we need to do is think about what we are trying to do. We are trying to find out if there are any duplicate numbers in the array. So, we need to find a way to keep track of the numbers we have seen before and if we have seen a number before, then we know that there is a duplicate.

Now that we have some direction we can start writing some code.

```py
def containsDuplicate(self, nums: List[int]) -> bool:
    seen = {} # Create a map

    # Loop through every element in the array
    for num in nums:
```

When we loop through every number in the array, we need to check if we have seen the number before. If we have, then we know that there is a duplicate. If we haven't, then we need to add it to the map.

```py
def containsDuplicate(self, nums: List[int]) -> bool:
    seen = {} # Create a map

    # Loop through every element in the array
    for num in nums:
        if num in seen:
            return True # If we have seen the number before, then return True
        else:
            # If we haven't seen the number before, then add it to the map
            seen[num] = 231
```

One funny thing you may see here is that I set the value of the key to `231`. This is because I don't care what the value is, I just care that the key exists. So, I just set it to some random number. The only thing that matters in this problem is how fast the map is which we know from previous discussion is \\(O(1)\\) or **constant time**.

So, now we have a solution to the problem. Let's look at the C++ solution.

```cpp
bool containsDuplicate(vector<int>& nums) {
    unordered_map<int, int> seen; // Create a map

    // Loop through every element in the array
    for (int num : nums) {
        if (seen.find(num) != seen.end()) {
            return true; // If we have seen the number before, then return True
        } else {
            // If we haven't seen the number before, then add it to the map
            seen[num] = 231;
        }
    }
}
```

The C++ solution is very similar to the Python solution. The only difference is that we have to use the `find` function to check if the key exists in the map. If the key exists, then the `find` function will return an pointer to the key. If the key does not exist, then the `find` function will return an pointer to the end of the map.

By using the `seen.find(num) != seen.end()`, we are just checking to see if the key exists in the map.


**Oops**! I forgot to return `false` if there are no duplicates. Let's fix that.

Here are the final solutions:

```py
def containsDuplicate(self, nums: List[int]) -> bool:
    seen = {} # Create a map

    # Loop through every element in the array
    for num in nums:
        if num in seen:
            return True # If we have seen the number before, then return True
        else:
            # If we haven't seen the number before, then add it to the map
            seen[num] = 231
    
    return False
```

```cpp
bool containsDuplicate(vector<int>& nums) {
    unordered_map<int, int> seen; // Create a map

    // Loop through every element in the array
    for (int num : nums) {
        if (seen.find(num) != seen.end()) {
            return true; // If we have seen the number before, then return True
        } else {
            // If we haven't seen the number before, then add it to the map
            seen[num] = 231;
        }
    }

    return false;
}
```

### Two Sum Problem

[Link on Leetcode](https://leetcode.com/problems/two-sum/)

> Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

This is a much harder problem that the one before. We are asked to find two numbers in the array that add up to the target and return their indices. 

> *indices* means that we need to return the **index** of the two numbers that add up to the target.

Okay, so how can we use a map to solve this problem?

Let's dive into a little arithmetic. If we have two numbers, \\(a\\) and \\(b\\).

We know that \\(a + b = t\\), but if we subtract \\(a\\) from both sides we get \\(b = t - a\\).

So, if we know what \\(a\\) is, then we can find \\(b\\) by subtracting \\(a\\) from \\(t\\).

This is super important to remember because this is how we are going to solve this problem.

Let's look at the code.

```py
def twoSum(self, nums: List[int], target: int) -> List[int]:

    # Loop through every element in the array
    for i in range(len(nums)):
        num = nums[i] # Get the current number
        complement = target - num # Get the complement of the current number
```

Now for each iteration of the loop, we have caluculated \\(b\\) (the complement). All we have to do now is check and see if that complement exists in the array.

Using a map, we can add every number in the array to the map. Then, when we are looping through the array, we can check and see if the complement exists in the map.

```py
def twoSum(self, nums: List[int], target: int) -> List[int]:
    seen = {} # Create a map

    # Loop through every element in the array
    for i in range(len(nums)):
        num = nums[i] # Get the current number
        complement = target - num # Get the complement of the current number

        if complement in seen:
            # If the complement exists in the map, then return the indices
            return [seen[complement], i]
        else:
            # If the complement does not exist in the map, 
            # then add the current number to the map
            seen[num] = i 
```

We check to see if the complement has already been seen in the array. If it has, then we know that the complement and the current number add up to the target. So, we return the indices of the complement and the current number. Luckily, we have the index of the complement stored in the map as the value!. We can just return that and the current index.

In this problem we actually made use of the map's value instead of setting it to a random value. This is because we need to return the index of the complement, and the only way to do that is to store it in the map.

Here is the C++ solution:

```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> seen; // Create a map

    // Loop through every element in the array
    for (int i = 0; i < nums.size(); i++) {
        int num = nums[i]; // Get the current number
        int complement = target - num; // Get the complement of the current number

        if (seen.find(complement) != seen.end()) {
            // If the complement exists in the map, then return the indices
            return {seen[complement], i};
        } else {
            // If the complement does not exist in the map, 
            // then add the current number to the map
            seen[num] = i;
        }
    }
}
```

This solution is a super fast solution to find two numbers that sum to equal `target`. Our solution runs in **linear time**, \\(O(n)\\), which means it is dependent on how large the array is. This is the fastest time possible for this problem.

## Conclusion

You've just been speedrun through some basic programming concepts and even solved some problems! I hope you learned something new and are excited to learn more.

If you have any questions, feel free to reach out on our Discord or direct message one of the officers. We are always happy to help!