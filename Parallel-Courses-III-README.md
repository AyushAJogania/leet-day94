# leet-day94

# Minimum Time to Complete All Courses

## Problem Description

You are given an integer `n`, indicating that there are `n` courses labeled from 1 to `n`. You are also given a 2D integer array `relations`, where `relations[j] = [prevCoursej, nextCoursej]` denotes that course `prevCoursej` has to be completed before course `nextCoursej` (a prerequisite relationship). Furthermore, you are given a 0-indexed integer array `time`, where `time[i]` denotes how many months it takes to complete the (i+1)th course.

The problem is to find the minimum number of months needed to complete all the courses while following these rules:

1. You may start taking a course at any time if the prerequisites are met.
2. Any number of courses can be taken at the same time.

Return the minimum number of months needed to complete all the courses.

**Note**: The test cases are generated such that it is possible to complete every course (i.e., the graph is a directed acyclic graph).

## Example

```plaintext
Input: n = 3, relations = [[1,3],[2,3]], time = [3,2,5]
Output: 8
Explanation: 
We start course 1 and course 2 simultaneously at month 0.
Course 1 takes 3 months, and course 2 takes 2 months to complete, respectively.
Thus, the earliest time we can start course 3 is at month 3, and the total time required is 3 + 5 = 8 months.
```

```plaintext
Input: n = 5, relations = [[1,5],[2,5],[3,5],[3,4],[4,5]], time = [1,2,3,4,5]
Output: 12
Explanation: 
You can start courses 1, 2, and 3 at month 0.
You can complete them after 1, 2, and 3 months, respectively.
Course 4 can be taken only after course 3 is completed, i.e., after 3 months. It is completed after 3 + 4 = 7 months.
Course 5 can be taken only after courses 1, 2, 3, and 4 have been completed, i.e., after max(1,2,3,7) = 7 months.
Thus, the minimum time needed to complete all the courses is 7 + 5 = 12 months.
```

## Constraints

- 1 <= n <= 50,000
- 0 <= relations.length <= min(n * (n - 1) / 2, 50,000)
- relations[j].length == 2
- 1 <= prevCoursej, nextCoursej <= n
- prevCoursej != nextCoursej
- time.length == n
- 1 <= time[i] <= 10,000
- The given graph is a directed acyclic graph.

## Solution Approach

The solution to this problem involves modeling the problem as a directed acyclic graph (DAG) with nodes representing courses and edges representing prerequisite relationships. Then, it calculates the minimum time required to complete all courses by finding the longest path in the DAG.

Here are the key steps in the solution approach:

1. Convert the given list of prerequisites (`relations`) into a DAG. Identify the starting nodes (courses with no prerequisites) and build the graph.

2. Define a recursive function to calculate the time required to complete a course. This function finds the maximum time needed for all prerequisites and adds the time for the current course. Memoization is used to avoid redundant calculations.

3. Iterate over all starting nodes (courses with no prerequisites) and calculate the time required for each. Keep track of the maximum time among these starting nodes, which represents the minimum time needed to complete all courses.

4. Return the maximum time as the answer.

## Complexity Analysis

The time and space complexity of this solution is as follows:

- **Time Complexity**: O(N + E), where N is the number of courses and E is the number of prerequisite relationships. The function that constructs the DAG takes O(E) time, and the function to calculate the maximum time takes O(N) time.

- **Space Complexity**: O(N + E), where N is the space for storing the nodes and E is the space for storing the edges in the DAG.

