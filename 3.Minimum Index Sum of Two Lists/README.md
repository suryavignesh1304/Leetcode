<h1>Minimum Index Sum of Two Lists</h1>

<h2>Problem Statement</h2>

<p>Given two arrays of strings <code>list1</code> and <code>list2</code>, find the common strings with the least index sum.</p>

<p>A common string is a string that appeared in both <code>list1</code> and <code>list2</code>.</p>

<p>A common string with the least index sum is a common string such that if it appeared at <code>list1[i]</code> and <code>list2[j]</code>, then <code>i + j</code> should be the minimum value among all other common strings.</p>

<p>Return all the common strings with the least index sum. Return the answer in any order.</p>

<h3>Example 1:</h3>
<ul>
    <li><strong>Input</strong>: <code>list1 = ["Shogun", "Tapioca Express", "Burger King", "KFC"]</code>, <code>list2 = ["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]</code></li>
    <li><strong>Output</strong>: <code>["Shogun"]</code></li>
    <li><strong>Explanation</strong>: The only common string is <code>"Shogun"</code>.</li>
</ul>

<h3>Example 2:</h3>
<ul>
    <li><strong>Input</strong>: <code>list1 = ["Shogun", "Tapioca Express", "Burger King", "KFC"]</code>, <code>list2 = ["KFC", "Shogun", "Burger King"]</code></li>
    <li><strong>Output</strong>: <code>["Shogun"]</code></li>
    <li><strong>Explanation</strong>: The common string with the least index sum is <code>"Shogun"</code> with index sum <code>0 + 1 = 1</code>.</li>
</ul>

<h3>Example 3:</h3>
<ul>
    <li><strong>Input</strong>: <code>list1 = ["happy", "sad", "good"]</code>, <code>list2 = ["sad", "happy", "good"]</code></li>
    <li><strong>Output</strong>: <code>["sad", "happy"]</code></li>
    <li><strong>Explanation</strong>: There are three common strings: <code>"happy"</code> with index sum <code>0 + 1 = 1</code>, <code>"sad"</code> with index sum <code>1 + 0 = 1</code>, and <code>"good"</code> with index sum <code>2 + 2 = 4</code>. The strings with the least index sum are <code>"sad"</code> and <code>"happy"</code>.</li>
</ul>

<h2>Constraints</h2>
<ul>
    <li><code>1 <= list1.length, list2.length <= 1000</code></li>
    <li><code>1 <= list1[i].length, list2[i].length <= 30</code></li>
    <li><code>list1[i]</code> and <code>list2[i]</code> consist of spaces and English letters.</li>
    <li>All the strings of <code>list1</code> and <code>list2</code> are unique.</li>
    <li>There is at least one common string between <code>list1</code> and <code>list2</code>.</li>
</ul>

<h2>Solution</h2>

<h3>Brute Force Approach</h3>

<p>This approach checks each string in <code>list1</code> with every string in <code>list2</code>. If they match, we calculate the sum of their indices. If the sum is the smallest we've seen so far, we update the result list. If the sum matches the smallest seen, we append the string to the result list.</p>

<pre>
<code>class Solution:
    def findRestaurant(self, list1: list[str], list2: list[str]) -> list[str]:
        min_sum = float('inf')
        result = []
        for i in range(len(list1)):
            for j in range(len(list2)):
                if list1[i] == list2[j]:
                    if (i + j) < min_sum:
                        min_sum = (i + j)
                        result = [list1[i]]
                    elif (i + j) == min_sum:
                        result.append(list1[i])
        return result
</code>
</pre>

<p>Time Complexity: <code>O(n * m)</code>, where <code>n</code> and <code>m</code> are the lengths of <code>list1</code> and <code>list2</code> respectively.</p>

<h3>Hash Table Approach</h3>

<p>To optimize the solution, we can use a hash table (or dictionary) to store the index positions of strings in both lists. Then, for each common string, we calculate the index sum and keep track of the minimum.</p>

<pre>
<code>class Solution:
    def findRestaurant(self, list1: list[str], list2: list[str]) -> list[str]:
        indexes1 = {list1[i]: i for i in range(len(list1))}
        indexes2 = {list2[i]: i for i in range(len(list2))}
        mini = len(list1) + len(list2)
        ans = []
        for str1, index1 in indexes1.items():
            if str1 in indexes2:
                index2 = indexes2[str1]
                if index1 + index2 < mini:
                    mini = index1 + index2
                    ans = [str1]
                elif index1 + index2 == mini:
                    ans.append(str1)
        return ans
</code>
</pre>

<p>In this approach, we:</p>
<ul>
    <li>First store the index of each string in both <code>list1</code> and <code>list2</code> using dictionaries.</li>
    <li>Then, for each common string, we calculate the index sum.</li>
    <li>If the current index sum is smaller than the minimum, we update the result list.</li>
    <li>If it equals the minimum, we append the string to the result list.</li>
</ul>

<h2>Complexity Analysis</h2>
<ul>
    <li><strong>Time Complexity</strong>: <code>O(n + m)</code> - where <code>n</code> and <code>m</code> are the lengths of <code>list1</code> and <code>list2</code> respectively. We iterate through both lists once.</li>
    <li><strong>Space Complexity</strong>: <code>O(n + m)</code> - Space is used for storing the index positions of strings from both lists.</li>
</ul>
