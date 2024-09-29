
<h1>Convert Integer to the Sum of Two No-Zero Integers</h1>

<h2>Problem Statement</h2>

<p>No-Zero integer is a positive integer that does not contain any 0 in its decimal representation.</p>

<p>Given an integer <code>n</code>, return a list of two integers <code>[a, b]</code> where:</p>

<ul>
    <li><code>a</code> and <code>b</code> are No-Zero integers.</li>
    <li><code>a + b = n</code>.</li>
</ul>

<p>The test cases are generated so that there is at least one valid solution. If there are many valid solutions, you can return any of them.</p>

<h3>Example 1:</h3>
<ul>
    <li><strong>Input</strong>: <code>n = 2</code></li>
    <li><strong>Output</strong>: <code>[1, 1]</code></li>
    <li><strong>Explanation</strong>: Let <code>a = 1</code> and <code>b = 1</code>. Both <code>a</code> and <code>b</code> are no-zero integers, and <code>a + b = 2</code> = <code>n</code>.</li>
</ul>

<h3>Example 2:</h3>
<ul>
    <li><strong>Input</strong>: <code>n = 11</code></li>
    <li><strong>Output</strong>: <code>[2, 9]</code></li>
    <li><strong>Explanation</strong>: Let <code>a = 2</code> and <code>b = 9</code>. Both <code>a</code> and <code>b</code> are no-zero integers, and <code>a + b = 11</code> = <code>n</code>. There are other valid answers such as <code>[8, 3]</code> that are also accepted.</li>
</ul>

<h2>Constraints</h2>
<ul>
    <li><code>2 <= n <= 10<sup>4</sup></code></li>
</ul>

<h2>Solution</h2>

<p>The key to solving this problem is to ensure that both <code>a</code> and <code>b</code> are no-zero integers, meaning their decimal representation does not contain the digit 0. We can use a simple loop to iterate through possible values of <code>a</code> from 1 to <code>n-1</code>, and for each value of <code>a</code>, we calculate <code>b = n - a</code>. If both <code>a</code> and <code>b</code> do not contain any 0, we return them as the solution.</p>

<p>The approach involves:</p>
<ul>
    <li>Looping from <code>1</code> to <code>n</code> and checking both <code>i</code> and <code>n-i</code> for the presence of zeros.</li>
    <li>If both numbers do not contain any zeros, return them as the result.</li>
</ul>

<pre>
<code>class Solution:
    def getNoZeroIntegers(self, n: int) -> list[int]:
        for i in range(1 , n):
            if ('0' not in str(i)) and ('0' not in str(n-i)):
                return [i , n - i]
</code>
</pre>

<p>In this approach:</p>
<ul>
    <li>We iterate through each possible pair <code>[i, n - i]</code>.</li>
    <li>Convert both <code>i</code> and <code>n - i</code> to strings and check if either contains the digit 0.</li>
    <li>If both numbers are no-zero integers, we return them as the solution.</li>
</ul>

<h2>Complexity Analysis</h2>
<ul>
    <li><strong>Time Complexity</strong>: <code>O(n log n)</code> - Iterating through <code>1</code> to <code>n</code>, and each conversion to string takes logarithmic time.</li>
    <li><strong>Space Complexity</strong>: <code>O(1)</code> - We are only using a constant amount of space to store the result.</li>
</ul>

