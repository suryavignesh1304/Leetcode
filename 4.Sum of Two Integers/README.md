<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sum of Two Integers</title>
</head>
<body>

<h1>Sum of Two Integers</h1>

<h2>Problem Statement</h2>

<p>Given two integers <code>a</code> and <code>b</code>, return the sum of the two integers without using the operators <code>+</code> and <code>-</code>.</p>

<h3>Example 1:</h3>
<ul>
    <li><strong>Input</strong>: <code>a = 1</code>, <code>b = 2</code></li>
    <li><strong>Output</strong>: <code>3</code></li>
</ul>

<h3>Example 2:</h3>
<ul>
    <li><strong>Input</strong>: <code>a = 2</code>, <code>b = 3</code></li>
    <li><strong>Output</strong>: <code>5</code></li>
</ul>

<h2>Constraints</h2>
<ul>
    <li><code>-1000 <= a, b <= 1000</code></li>
</ul>

<h2>Solution</h2>

<h3>Approach</h3>

<p>To solve this problem, we can use bit manipulation techniques instead of the traditional arithmetic operations <code>+</code> and <code>-</code>. The idea is to simulate the behavior of addition using bitwise operations, specifically XOR, AND, and left shift.</p>

<h3>Steps</h3>

<ol>
    <li><strong>XOR</strong> (<code>^</code>): The XOR operation between <code>a</code> and <code>b</code> gives us the sum without considering the carry.</li>
    <li><strong>AND</strong> (<code>&</code>): The AND operation between <code>a</code> and <code>b</code> gives us the carry bits.</li>
    <li><strong>Left Shift</strong> (<code><<</code>): The carry is shifted left to add it in the correct position in the sum.</li>
    <li>The process repeats until there is no carry.</li>
</ol>

<p>To handle both positive and negative integers, we use masking to simulate 32-bit integer overflow behavior in Python.</p>

<h3>Python Code</h3>

<pre>
<code>class Solution:
    def getSum(self, a: int, b: int) -> int:
        MASK = 0xFFFFFFFF  # Mask to simulate 32-bit overflow
        MAX_INT = 0x7FFFFFFF  # Maximum value for a 32-bit integer

        while b != 0:
            carry = (a & b) & MASK  # Calculate carry bits
            a = (a ^ b) & MASK  # Calculate sum without carry
            b = (carry << 1) & MASK  # Shift carry to the left

        # Handle overflow by converting to negative if needed
        if a > MAX_INT:
            a = ~(a ^ MASK)  # Convert 32-bit result back to negative
        return a
</code>
</pre>

<h2>Explanation</h2>

<ul>
    <li><code>MASK = 0xFFFFFFFF</code>: This is used to keep the results within the 32-bit integer range.</li>
    <li><code>MAX_INT = 0x7FFFFFFF</code>: This is the maximum value for a 32-bit signed integer.</li>
    <li><strong>While loop:</strong> We continue the loop as long as there is a carry (i.e., <code>b != 0</code>). Within each iteration:
        <ul>
            <li><code>carry = (a & b) & MASK</code>: This calculates the carry bits (i.e., the bits that would "carry over" to the next position when adding the numbers).</li>
            <li><code>a = (a ^ b) & MASK</code>: This calculates the sum of <code>a</code> and <code>b</code> without considering the carry bits.</li>
            <li><code>b = (carry << 1) & MASK</code>: This shifts the carry bits to the left by one, preparing them to be added in the next iteration.</li>
        </ul>
    </li>
    <li>Finally, after the loop completes, we check if the result exceeds the 32-bit signed integer range. If <code>a > MAX_INT</code>, we convert <code>a</code> to a negative number using bitwise negation.</li>
</ul>

<h2>Complexity Analysis</h2>

<ul>
    <li><strong>Time Complexity</strong>: <code>O(1)</code> - The loop runs a fixed number of times (at most 32 iterations for 32-bit integers), so the time complexity is constant.</li>
    <li><strong>Space Complexity</strong>: <code>O(1)</code> - We use a constant amount of extra space for variables.</li>
</ul>

</body>
</html>
