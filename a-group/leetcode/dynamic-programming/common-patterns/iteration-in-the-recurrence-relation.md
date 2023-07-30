# Iteration in the recurrence relation

In all the problems we have looked at so far, the recurrence relation is a static equation - it never changes. Recall [Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/). The recurrence relation was:

\text{dp(i)} = \min( \text{dp(i - 1) + cost\[i - 1], dp(i - 2) + cost\[i - 2]})dp(i)=min(dp(i - 1) + cost\[i - 1], dp(i - 2) + cost\[i - 2])

because we are only allowed to climb 1 or 2 steps at a time. What if the question was rephrased so that we could take up to \text{k}k steps at a time? The recurrence relation would become dynamic - it would be:

\text{dp(i)} = \min( \text{dp(j) + cost\[j])}dp(i)=min(dp(j) + cost\[j]) for all \text{(i - k)} \leq \text{j} < \text{i}(i - k)≤j\<i

We would need iteration in our recurrence relation.

This is a common pattern in DP problems, and in this chapter, we're going to take a look at some problems using the framework where this pattern is applicable. While iteration usually increases the difficulty of a DP problem, particularly with bottom-up implementations, the idea isn't too complicated. Instead of choosing from a static number of options, we usually add a for-loop to iterate through a dynamic number of options and choose the best one.

## Example 1335. Minimum Difficulty of a Job Schedule



> We'll start with a top-down approach.

In this article, we'll be using the framework to solve [Minimum Difficulty of a Job Schedule](https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule/). We can tell this is a problem where Dynamic Programming can be used because we are asked for the minimum of something, and deciding how many jobs to do on a given day affects the jobs we can do on all future days. Let's start solving:

1\. A **function** that answers the problem for a given state

Let's first decide on state variables. What decisions are there to make, and what information do we need to make these decisions? Reading the problem description carefully, there are \text{d}d total days, and on each day we need to complete some number of jobs. By the end of the \text{d}d days, we must have finished all jobs (in the given order). Therefore, we can see that on each day, we need to decide how many jobs to take.

* Let's use one state variable \text{i}i, where \text{i}i is the index of the first job that will be done on the current day.
* Let's use another state variable \text{day}day, where \text{day}day indicates what day it currently is.

The problem is asking for the minimum difficulty, so let's have a function \text{dp(i, day)}dp(i, day) that returns the minimum difficulty of a job schedule which starts on the i^{th}ith job and day, \text{day}day. To solve the original problem, we will just return \text{dp(0, 1)}dp(0, 1), since we start on the first day with no jobs done yet.

![](https://leetcode.com/explore/learn/card/Figures/DP1/C3A2\_1\_cropped.png)\
![](https://leetcode.com/explore/learn/card/Figures/DP1/C3A2\_2\_cropped.png)\


2\. A **recurrence relation** to transition between states

At each state, we are on day \text{day}day and need to do job \text{i}i. Then, we can choose to do a few more jobs. How many more jobs are we allowed to do? The problem says that we need to do at least one job per day. This means we **must** leave at least \text{d - day}d - day jobs so that all the future days have at least one job that can be scheduled on that day. If \text{n}n is the total number of jobs, \text{jobDifficulty.length}jobDifficulty.length, that means from any given state \text{(i, day)}(i, day), we are allowed to do the jobs from index \text{i}i up to but not including index \text{n - (d - day)}n - (d - day).

We should try all the options for a given day - try doing only one job, then two jobs, etc. until we can't do any more jobs. The best option is the one that results in the easiest job schedule.

The difficulty of a given day is the most difficult job that we did that day. Since the jobs have to be done in order, if we are trying all the jobs we are allowed to do on that day (iterating through them), then we can use a variable \text{hardest}hardest to keep track of the difficulty of the hardest job done today. If we choose to do jobs up to the j^{th}jth job (inclusive), where \text{i} \leq \text{j} < \text{n - (d - day)}i≤j\<n - (d - day) (as derived above), then that means on the next day, we start with the (j + 1)^{th}(j+1)th job. Therefore, our total difficulty is \text{hardest + dp(j + 1, day + 1)}hardest + dp(j + 1, day + 1). This gives us our scariest recurrence relation so far:

\text{dp(i, day) = min(hardest + dp(j + 1, day + 1))}dp(i, day) = min(hardest + dp(j + 1, day + 1)) for all \text{i} \leq \text{j} < \text{n - (d - day)}i≤j\<n - (d - day), where \text{hardest = max(jobDifficulty\[k])}hardest = max(jobDifficulty\[k]) for all \text{i} \leq \text{k} \leq \text{j}i≤k≤j.

The codified recurrence relation is a scary one to look at for sure. However, it is easier to understand when we break it down bit by bit. On each day, we try all the options - do only one job, then two jobs, etc. until we can't do any more (since we need to leave some jobs for future days). \text{hardest}hardest is the hardest job we do on the current day, which means it is also the difficulty of the current day. We add \text{hardest}hardest to the next state which is the next day, starting with the next job. After trying all the jobs we are allowed to do, choose the best result.

![Current](blob:https://leetcode.com/1c97d4ef-f0cc-4462-b49d-3396d1f4fddd)1 / 3

\


3\. **Base cases**

Despite the recurrence relation being complicated, the base cases are much simpler. We need to finish all jobs in \text{d}d days. Therefore, if it is the last day (\text{day == d}day == d), we need to finish up all the remaining jobs on this day, and the total difficulty will just be the largest number in \text{jobDifficulty}jobDifficulty on or after index \text{i}i.

\text{if day == d}if day == d then return the maximum job difficulty between job \text{i}i and the end of the array (inclusive).

We can precompute an array \text{hardestJobRemaining}hardestJobRemaining where \text{hardestJobRemaining\[i]}hardestJobRemaining\[i] represents the difficulty of the hardest job on or after day \text{i}i, so that we this base case is handled in constant time.

Additionally, if there are more days than jobs (\text{n < d}n < d), then it is impossible to do at least one job each day, and per the problem description, we should return \text{-1}-1. We can check for this case at the very start.

\


#### Top-down Implementation <a href="#top-down-implementation" id="top-down-implementation"></a>

Let's combine these 3 parts for a top-down implementation. Again, we will use [functools](https://docs.python.org/3/library/functools.html) in Python, and a 2D array in Java for memoization. In the Python implementation, we are passing \text{None}None to `lru_cache` which means the cache size is not limited. We are doing this because the number of states that will be re-used in this problem is large, and we don't want to evict a state early and have to re-calculate it.

```java
class Solution {
    private int n, d;
    private int[][] memo;
    private int[] jobDifficulty;
    private int[] hardestJobRemaining;
    
    private int dp(int i, int day) {
        // Base case, it's the last day so we need to finish all the jobs
        if (day == d) {
            return hardestJobRemaining[i];
        }
        
        if (memo[i][day] == 0) {
            int best = Integer.MAX_VALUE;
            int hardest = 0;
            // Iterate through the options and choose the best
            for (int j = i; j < n - (d - day); j++) {
                hardest = Math.max(hardest, jobDifficulty[j]);
                // Recurrence relation
                best = Math.min(best, hardest + dp(j + 1, day + 1));
            }
            memo[i][day] = best;
        }
        
        return memo[i][day];
    }
    
    public int minDifficulty(int[] jobDifficulty, int d) {
        n = jobDifficulty.length;
        // If we cannot schedule at least one job per day, 
        // it is impossible to create a schedule
        if (n < d) {
            return -1;
        }
        
        hardestJobRemaining = new int[n];
        int hardestJob = 0;
        for (int i = n - 1; i >= 0; i--) {
            hardestJob = Math.max(hardestJob, jobDifficulty[i]);
            hardestJobRemaining[i] = hardestJob;
        }
        
        this.d = d;
        this.jobDifficulty = jobDifficulty;
        memo = new int[n][d + 1];
        return dp(0, 1);
    }
}
```

#### Bottom-up Implementation <a href="#bottom-up-implementation" id="bottom-up-implementation"></a>

With bottom-up, we now use a 2D array where \text{dp\[i]\[day]}dp\[i]\[day] represents the minimum difficulty of a job schedule that starts on day \text{day}day and job \text{i}i. It depends on the problem, but the bottom-up code generally has a faster runtime than its top-down equivalent. However, as you can see from the code, it looks like it is more challenging to implement. We need to first tabulate the base case and then work backwards from them using nested for loops.

The for-loops should start iterating from the base cases, and there should be one for-loop for each state variable. Remember that one of our base cases is that on the final day, we need to complete all jobs. Therefore, our for-loop iterating over \text{day}day should iterate from the final day to the first day. Then, our next for-loop for \text{i}i should conform to the restraints of the problem - we need to do at least one job per day.

```java
class Solution {
    public int minDifficulty(int[] jobDifficulty, int d) {
        int n = jobDifficulty.length;
        // If we cannot schedule at least one job per day, 
        // it is impossible to create a schedule
        if (n < d) {
            return -1;
        }
        
        int dp[][] = new int[n][d + 1];
        for (int[] row: dp) {
            Arrays.fill(row, Integer.MAX_VALUE);
        }
        
        // Set base cases
        dp[n - 1][d] = jobDifficulty[n - 1];

        // On the last day, we must schedule all remaining jobs, so dp[i][d]
        // is the maximum difficulty job remaining
        for (int i = n - 2; i >= 0; i--) {
            dp[i][d] = Math.max(dp[i + 1][d], jobDifficulty[i]);
        }
        
        for (int day = d - 1; day > 0; day--) {
            for (int i = day - 1; i < n - (d - day); i++) {
                int hardest = 0;
                // Iterate through the options and choose the best
                for (int j = i; j < n - (d - day); j++) {
                    hardest = Math.max(hardest, jobDifficulty[j]);
                    // Recurrence relation
                    dp[i][day] = Math.min(dp[i][day], hardest + dp[j + 1][day + 1]);
                }
            }
        }
        
        return dp[0][1];
    }
}
```

