<h1>Two Sum Problem</h1>

<h2>Problem Statement</h2>

<p>Given an array of integers <code>nums</code> and an integer <code>target</code>, return the indices of the two numbers such that they add up to the target.</p>

<p>You may assume that each input will have exactly one solution, and you may not use the same element twice.</p>

<p>You can return the answer in any order.</p>

<h3>Example 1:</h3>
<ul>
    <li><strong>Input</strong>: <code>nums = [2, 7, 11, 15]</code>, <code>target = 9</code></li>
    <li><strong>Output</strong>: <code>[0, 1]</code></li>
    <li><strong>Explanation</strong>: Because <code>nums[0] + nums[1] == 9</code>, we return <code>[0, 1]</code>.</li>
</ul>

<h3>Example 2:</h3>
<ul>
    <li><strong>Input</strong>: <code>nums = [3, 2, 4]</code>, <code>target = 6</code></li>
    <li><strong>Output</strong>: <code>[1, 2]</code></li>
</ul>

<h3>Example 3:</h3>
<ul>
    <li><strong>Input</strong>: <code>nums = [3, 3]</code>, <code>target = 6</code></li>
    <li><strong>Output</strong>: <code>[0, 1]</code></li>
</ul>

<h2>Brute Force Approach</h2>

<p>The brute force solution checks every pair of numbers in the array to see if they sum up to the target. The time complexity for this approach is <code>O(n²)</code> because it uses nested loops.</p>

<pre>
<code>class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        for i in range(len(nums)):
            for j in range(i + 1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
        return []
</code>
</pre>

<p>Although this approach works, it is inefficient for large input sizes as it runs in quadratic time.</p>

<h2>Optimized Approach Using a Hash Table</h2>

<p>To improve the efficiency, we can use a hash table (or dictionary) to store the numbers and their indices. By doing this, we can check if the complement (target - current number) already exists in the hash table in constant time. This reduces the time complexity to <code>O(n)</code>.</p>

<pre>
<code>class Solution:
    def twoSum(self, nums, target):
        nums_dict = {}
        for i in range(len(nums)):
            nums_dict[nums[i]] = i
        
        for i in range(len(nums)):
            rem = target - nums[i]
            if rem in nums_dict and i != nums_dict[rem]:
                return [i, nums_dict[rem]]
</code>
</pre>

<p>In this optimized approach:</p>
<ul>
    <li>We first iterate through the array once, storing each number's index in the dictionary <code>nums_dict</code>.</li>
    <li>Then, in another loop, we calculate the complement (remaining value) for each number and check if it already exists in the dictionary.</li>
    <li>If the complement exists and isn't the same as the current index, we return the pair of indices.</li>
</ul>

<h2>Complexity Analysis</h2>
<ul>
    <li><strong>Time Complexity</strong>: <code>O(n)</code> - We traverse the array twice, but each lookup in the hash table is O(1).</li>
    <li><strong>Space Complexity</strong>: <code>O(n)</code> - We store each number and its index in the hash table.</li>
</ul>
