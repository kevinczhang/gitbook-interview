# OA 1



今早刚做的OA, 全是地里原题。第一题：Maximum Number of Engineering Teams 第二题：Maximum password strength‌‌‌‌‍， e.g. "good" 的strength 是16 然后尴尬的是，因为在地里看到过最优解，上来就写代码很快all test cases passed 就提交了, 最后OA结束后系统秒通知phone interview。 所有的test cases 都过了啊，解法也是O(N)的，不懂为啥加了一轮phone，以为系统检测我写得太快了？😭 玄学。。 最后附上自己总结的近期OA高频，希望更给地里小伙伴节省时间：

1. Group Digits: https://leetcode.com/discuss/int ... 021-grouping-digits
2. Maximum Number of Engineering Teams： https://leetcode.com/discuss/interview-question/1688196
3. Group movies with awards https://leetcode.com/discuss/int ... 5633/Amazon-OA-2022 和max number engineering team 很像， greedy algorithm
4. LC926 Flip String to Monotone Increasing 5.  LC2104. Sum of Subarray Ranges
5. Maximum password strength‌‌‌‌‍ https://leetcode.com/discuss/interview-question/1526418/ https://leetcode.com/discuss/int ... a-password-strength
6. Optimal Utilization (Aircraft) https://leetcode.com/discuss/interview-question/373202
7. maximum quality sent via a channel https://leetcode.com/discuss/int ... the-server-channels 注意：Edge case主要就是结果可能溢出的问题，累加median的时候存在long里就行了
8. valid coupon/valid string：    让判断每个coupon是否valid，就是decode string那个题套个场景，string valid的要求是xYx的形式，就是abba或者aba这种。这个大家之前也说过，就是用stack来记录之前见过的char，如果cur char和stack上的不一样就push，如果一样就pop，最后检查stack是不是为空 https://leetcode.com/discuss/int ... zon-oa-valid-string
9. Given an array of only 1 and -1, find a subarray of maximum length such that the product of all the elements in the subarray is 1 循环一遍，记录所以-1的位置。如果有偶数个-1就直接返回真个array。接下来就比较从array头到最后一个-1，和array尾到第一个-1，哪个更长。
10. numberofways (Alexa bookmark) https://leetcode.com/discuss/interview-question/1488281/Amazon-OA
11. LC1091. Shortest Path in Binary Matrix
12. 字符串里包含（，），【，】和？，求有几种分割方式能使两个子字符串都是balanced string, balanced string 是指两种括号的开和关数量相等，问号可以充当任意括号 https://leetcode.com/discuss/int ... y-2021-ios-engineer
13. 一个亚马逊用户评分数字list, 找有多少个decreasing sublist， 这里decreasing 一定要是一分一分降的，比如4，3就是3个， 4一个，3一个，43一个 https://leetcode.com/playground/P9doEn6x
14. LC937. Reorder Data in Log Files
15. 给一个string, 计算maximum deviation of all substrings. The maximum deviation 就是 difference between the maximum frequency of a character and the minimum frequency of a character. 举个例子, in “abcaba”, "a" 的频率是3; "b"的频率是2; "c" 的频率是1. 所以"a" 是最大频率, which is 3, “c” 是最小频率, which is 1. 最后的deviation of this string is 3-1 = 2. 然后这题问的是在所有的substring里，最大的deviation是多少。 https://leetcode.com/discuss/int ... mong-all-substrings
16. 算用电量，两个数字 list，一个是processing powder, 一个是booting power, 分别对应一个处理器，每个处理器先需要booting power用电量来启动，再需要对应的processing power来运行，现在可以把相邻的k处理器弄成一个cluster，总用电量= max(booting power among the k处理器）+ sum of processing power\*k, 再给一个最大值powerMax, 问最多可以把多少个处理器‍‌‌‌‌‍‌‌‌‍‍‍‌‍‍‌‍‌弄成一个cluster，总耗电小于最大值。 解法：TreeSet+Two pointer可能可以做？每次把右pointer前进，把当前的boot加入TreeSet，process加入window的sum，TreeSet可以nlogn找到最大的boot。如果超了就移动左边的pointer，从process sum和TreeSet里去掉被移出的machine。
17. getServedBuildings 路由器覆盖大楼的问题，问多少大楼可以被覆盖到（就是大楼内的租客人数 <= 这栋大楼被覆盖的路由数量） 常规思路解题可能会超时.
18. minimumDistance 就是从左上角出发，直到走到标为9的目的地。1 代‍‌‌‌‌‍‌‌‌‍‍‍‌‍‍‌‍‌表有路，0代表没有路。（BFS不会超时)
19. Lc56. Merge Intervals 问的是：最少merge几个区间, 返回的是int
20. Students ranks https://leetcode.com/discuss/int ... sde-2-february-2022
21.
    1. Kth Largest Element in a Stream 类似data stream找第k大。给一个list， 里面是item的可以“插入“也可以”浏览“， 第k次“浏览”要返回已插入的第k小的元素，元素包括名字和价格，要先按价格排序，再按名字排字典序。先用了两个heap的做法，但是有bug没时间改，最后用了暴力法有几个c‍‌‌‌‌‍‌‌‌‍‍‍‌‍‍‌‍‌ase tle。怕是凉了。
22. 给定一个数组表示package weight，如果p(i) < p(i+1) (必须严格小于)，表示两个包裹可以merge，新的包裹重量为两个包裹相加，原来的两个包裹被新包裹替换，可以无限次重复此操作，求最大可获得的包裹重量。 解法: 单调栈 一个单调递增栈 当遇到 比栈顶小的 就 把之前的 全部合并起来
23. Count Subarrays with Consecutive elements by minus1 https://www.geeksforgeeks.org/co ... nts-differing-by-1/ 另外感谢这两个帖子给我很多信息：point3acres.com/bbs/thread-816549-1-1.html https://www.1point3acres.com/bbs/thread-788096-1-1.html
