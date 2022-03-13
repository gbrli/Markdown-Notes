# Problem Solving and Patterns

An algorithm is a process or set of steps to accomplish a task. The two steps to solving a problem are devising a plan, and mastering common patterns.

## How to Solve it

There are five steps to solving any problem.

### 1 - Understand the problem

1. Restate the problem in my own words
2. Which inputs go into the problem?
3. Which outputs should come from the solution?
4. How can I determine the output from the input? Do I have all the information I need?
5. How should I label the data pieces that are part of the problem?

### 2 - Explore concrete examples

1. Create a simple example
2. Create a complex example
3. Explore them with empty inputs
4. Explore them with invalid inputs

### 3 - Break it down

1. Write out the steps you need to take in pseudocode so you can make sure the logic is correct and you can worry about syntax later

### 4 - Solve or simplify

1. find the core difficulty in the problem
2. Temporarily ignore it and start coding the rest
3. Write a simplified solution
4. Work your way up to the difficulty and implement it

### 5 - Look back and refactor

1. Does it work?
2. Can it work differently?
3. Is it easy to understand?
4. Can it be used for other problems?
5. Can it perform better?
6. Can you refactor differently?
7. How have other people solved the problem?

## Common Patterns

### Frequency counter

If two data sets (such as arrays) need to be compared, frequency counter is a common strategy.

1. Create two objects
2. Loop the arrays to be compared one at a time, and add them separate to the two different objects
3. Loop the first object and compare it to the second using if statements on the inside

Having multiple separate loops is always better than having a nested loop, and will result in `O(n)`.

### Multiple pointers

This method creates pointers that correspond to an index or position and then move towards the beginning, middle or end. It is necessary to have a sorted array for this approach.

1. Create two variables for each starting point
2. Loop over the array
3. Compare the two points
4. If it's a match return true, otherwise ++ one and -- the other, or something similar

### Sliding window

This method creates a window such as an array, or a number from a position to another. The window can increase, or it can close and create another window. It is useful for keep track of a subset of data.

1. Create two empty counting variables
2. Create a subarray by looping the original one and assign it to one variable
3. Copy it to the second variable
4. Loop over one of the variables following the window size
5. Move it forward or backwards one step by changing the index numbers

### Divide and conquer

This method divides a section of data and splits it in smaller steps repeatedly, until you find what you need. It works really well to reduce time complexity, but it can get wordy.

Other common strategies are dynamic programming, greedy algorithm, and backtracking.
