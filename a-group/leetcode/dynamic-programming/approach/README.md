# Approach

## Framework for DP Problems

Now that we understand the basics of DP and how to spot when DP is applicable to a problem, we've reached the most important part: actually solving the problem. In this section, we're going to talk about a framework for solving DP problems. This framework is applicable to nearly every DP problem and provides a clear step-by-step approach to developing DP algorithms.

> For this article's explanation, we're going to use the problem [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) as an example, with a top-down (recursive) implementation. Take a moment to read the problem description and understand what the problem is asking.

Before we start, we need to first define a term: **state**. In a DP problem, a **state** is a set of variables that can sufficiently describe a scenario. These variables are called **state variables**, and we only care about relevant ones. For example, to describe every scenario in Climbing Stairs, there is only 1 relevant state variable, the current step we are on. We can denote this with an integer \text{i}i. If \text{i = 6}i = 6, that means that we are describing the state of being on the 6th step. Every unique value of \text{i}i represents a unique **state**.

> You might be wondering what "relevant" means here. Picture this problem in real life: you are on a set of stairs, and you want to know how many ways there are to climb to say, the 10th step. We're definitely interested in what step you're currently standing on. However, we aren't interested in what color your socks are. You could certainly include sock color as a state variable. Standing on the 8th step wearing green socks is a different state than standing on the 8th step wearing red socks. However, changing the color of your socks will not change the number of ways to reach the 10th step from your current position. Thus the color of your socks is an **irrelevant** variable. In terms of figuring out how many ways there are to climb the set of stairs, the only **relevant** variable is what stair you are currently on.

\


#### The Framework <a href="#the-framework" id="the-framework"></a>

To solve a DP problem, we need to combine 3 things:

1.  **A function or data structure that will compute/contain the answer to the problem for every given state**.

    For Climbing Stairs, let's say we have an function \text{dp}dp where \text{dp(i)}dp(i) returns the number of ways to climb to the i^{th}ith step. Solving the original problem would be as easy as \text{return dp(n)}return dp(n).

    How did we decide on the design of the function? The problem is asking "How many distinct ways can you climb to the top?", so we decide that the function will represent how many distinct ways you can climb to a certain step - literally the original problem, but generalized for a given state.

    > Typically, top-down is implemented with a recursive function and hash map, whereas bottom-up is implemented with nested for loops and an array. When designing this function or array, we also need to decide on state variables to pass as arguments. This problem is very simple, so all we need to describe a state is to know what step we are currently on \text{i}i. We'll see later that other problems have more complex states.
2.  **A recurrence relation to transition between states.**

    A recurrence relation is an equation that relates different states with each other. Let's say that we needed to find how many ways we can climb to the 30th stair. Well, the problem states that we are allowed to take either 1 or 2 steps at a time. Logically, that means to climb to the 30th stair, we arrived from either the 28th or 29th stair. Therefore, the number of ways we can climb to the 30th stair is equal to the number of ways we can climb to the 28th stair plus the number of ways we can climb to the 29th stair.\
    \
    The problem is, we don't know how many ways there are to climb to the 28th or 29th stair. However, we can use the logic from above to define a recurrence relation. In this case, \text{dp(i) = dp(i - 1) + dp(i - 2)}dp(i) = dp(i - 1) + dp(i - 2). As you can see, information about some states gives us information about other states.

    > Upon careful inspection, we can see that this problem is actually the Fibonacci sequence in disguise! This is a very simple recurrence relation - typically, finding the recurrence relation is the most difficult part of solving a DP problem. We'll see later how some recurrence relations are much more complicated, and talk through how to derive them.
3.  **Base cases, so that our recurrence relation doesn't go on infinitely.**

    The equation \text{dp(i) = dp(i - 1) + dp(i - 2)}dp(i) = dp(i - 1) + dp(i - 2) on its known will continue forever to negative infinity. We need base cases so that the function will eventually return an actual number.\
    \
    Finding the base cases is often the easiest part of solving a DP problem, and just involves a little bit of logical thinking. When coming up with the base case(s) ask yourself: What state(s) can I find the answer to without using dynamic programming? In this example, we can reason that there is only 1 way to climb to the first stair (1 step once), and there are 2 ways to climb to the second stair (1 step twice and 2 steps once). Therefore, our base cases are \text{dp(1) = 1}dp(1) = 1 and \text{dp(2) = 2}dp(2) = 2.

    > We said above that we don't know how many ways there are to climb to the 28th and 29th stairs. However, using these base cases and the recurrence relation from step 2, we can figure out how many ways there are to climb to the 3rd stair. With that information, we can find out how many ways there are to climb to the 4th stair, and so on. Eventually, we will know how many ways there are to climb to the 28th and 29th stairs.

## Time and Space Complexity

Finding the time and space complexity of a dynamic programming algorithm may sound like a daunting task. However, this task is usually not as difficult as it sounds. Furthermore, justifying the time and space complexity in an explanation is relatively simple as well. One of the main points with DP is that we never repeat calculations, whether by tabulation or memoization, we only compute a state once. Because of this, the time complexity of a DP algorithm is directly tied to the number of possible states.

If computing each state requires FF time, and there are nn possible states, then the time complexity of a DP algorithm is O(n \cdot F)O(n⋅F). With all the problems we have looked at so far, computing a state has just been using a recurrence relation equation, which is O(1)O(1). Therefore, the time complexity has just been equal to the number of states. To find the number of states, look at each of your state variables, compute the number of values each one can represent, and then multiply all these numbers together.

Let's say we had 3 state variables: \text{i}i, \text{k}k, and \text{holding}holding for some made up problem. \text{i}i is an integer used to keep track of an index for an input array \text{nums}nums, \text{k}k is an integer given in the input which represents the maximum actions we can do, and \text{holding}holding is a boolean variable. What will the time complexity be for a DP algorithm that solves this problem? Let \text{n = nums.length}n = nums.length and \text{K}K be the maximum actions possible given in the input. \text{i}i can be from \text{0}0 to \text{nums.length}nums.length, \text{k}k can be from \text{0}0 to \text{K}K, and \text{holding}holding }can be true or false. Therefore, there are \text{n} \cdot \text{K} \cdot \text{2}n⋅K⋅2 states. If computing each state is O(1)O(1), then the time complexity will be O(n \cdot K \cdot 2) = O(n \cdot K)O(n⋅K⋅2)=O(n⋅K).

Whenever we compute a state, we also store it so that we can refer to it in the future. In bottom-up, we tabulate the results, and in top-down, states are memoized. Since we store states, the space complexity is equal to the number of states. That means that in problems where calculating a state is O(1)O(1), the time and space complexity are the same. In many DP problems, there are optimizations that can improve both complexities - we'll talk about this later.

\
