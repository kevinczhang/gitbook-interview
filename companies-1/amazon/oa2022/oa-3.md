# OA 3

5/2 OA 题目1：Maximum twin sum of a linked list 就是给你一个单向链表，让你求第一个和最后一个的sum，第二个和倒数第二个的sum，以此类推，返回这个sum的最大值。要求要用o(1)的空间。 做法很直接，找中点，断开连接，反转后半段链表，然后iterate。 题目2：Count subarray imbalance



题目2：Count subarray imbalance 这题我没在地里面找到过，所以准备的时候漏掉了。但是这里有https://leetcode.com/discuss/int ... t-imbalance-variant&#x20;

Given an int array of item weights and integer k, a segment of contiguously placed items can be shipped together if and only if the difference between the weights of the heaviest and lightest item differs by at most k to avoid load imbalance. find the number of the segment of items can be shipped together&#x20;

Note: a segment (l,r) is a subarray starts at l and ends at r&#x20;

Any clue? Edit: e.g.: input: k = 3; weights = \[1, 3, 6];&#x20;

weight difference between max and min for each (l,r) index pair are:&#x20;

(0,0) -> max(1) - min(1) = 1 - 1 = 0&#x20;

(0, 1) -> max(1, 3) - min(1, 3) = 3 - 1 = 2&#x20;

(0, 2) -> max(1, 3, 6) - min(1, 3, 6) = 6- 1 = 5 exceed k = 3&#x20;

(1, 1) -> max(3) - min(3) = 3- 3 = 0&#x20;

(1, 2) -> max(3, 6) - min(3, 6) = 6 - 3 = 3&#x20;

(2, 2) -> max(6) - min(6) = 6 - 6 = 0&#x20;

5 0f 6 segments have diff <= k, ans is 5&#x20;

I find this problem from a forum, there is no constraints information in that post, O(N^2) is easy to come up with, I assume the length of the array would be up to 10^5, so approach with O(NLogN) or O(N) would be preferred.&#x20;

以下是我用了两天时间准备的最近3个月的题目，以及我觉得还不错的解题思路和有些引用的帖子，以上的思路很多都是引用原作者的话。如果有侵权的话版主就删了吧。&#x20;

game 一滴血 Amazon prime is designing a game. the player needs to pass n rounds sequentially in this game. rules for the palyer are: The player loses power health to complete round i. the player's health must be greater than 0 at all times. the player can choose to use armor in any one round. the armor will prevent damage of min(armor,power). Determine the minimum starting health for a player to with the game&#x20;

Example:&#x20;

Power = \[1,2,6,7] armor = 5 Give the player 12 units of health at the beginning of the game. one of the optimal strategies is to use the armor in the third round and only lose 1 unit instead of 6.&#x20;

The health of the player after each round is 12&#x20;

12 - Power\[0] = 12 - 1 = 11&#x20;

11 - Power\[1] = 11 - 2 = 9&#x20;

9 - Power\[2] + armor = 9 - 6 + 5 = 8&#x20;

8 - Power\[3] = 8 - 7 = 1&#x20;

No lower starting health will allow a win. Complete the function findMinHealth in the editor below. int Power\[n]: health cost in each round int armor: the max amount of health that may be returnd one round only&#x20;

Returns: int: the minimum amount of health requiered at the beginig of the game def findMinHealth(power, armor): 直接贪心&#x20;

**Minimum Net stock price**&#x20;

https://codereview.stackexchange ... m-in-an-array-of-pr&#x20;

Given the stock prices of n months, the net price change for the i-th month is defined as the absolute difference between the average of stock prices for the first i months and for the remaining (n-i) months where 1 <= i < n. These averages are rounded down to an integer.&#x20;

Given an array of stock prices, find the month at which the net price change is minimum. If there are s‍‌‌‌‍‌‍‌‌‍‌‌‍‍‌‍‌‌‍‍everal such months, return the earliest month.&#x20;

Note: The average of a set of integers here is defined as the sum of integers divided by the number of integers, rounded down to the nearest integer.&#x20;

For example, the average of \[1,2,3,4] is the floor of (1 + 2 + 3 + 4) / 4 = 2.5 and the floor of 2.5 is 2.&#x20;

Example: stockPrice = \[1,3,2,3] The minimum net price change is 0, and it occurs in the 2nd month. Return 2.&#x20;

子序列平均值之差的最小值的划分 计算总和，遍历一遍计算后面部分的累加和，剩下的用总和减（从右往左）&#x20;

**股票平均最大值 max average stock price**&#x20;

给一个int数组，里面是股票, 全是正数，stock表示第i个月的股票。还有一个int k。问连续k个月的股票和的最大值。这连续k个月里不能有重复的数字。sliding window。注意返回值是long int， 如果用了int有隐藏的test case会过不了。 给一个长度为n的数组表示n个月的股价，给定k值，给连续k月并且k个值各不一样的区间求和，找到最大和。例子：｛1，2，3，4｝，k=2，那总共有(1,2) (2,3)(3,4)三个长度为k的连续区间并且每个区间没有重复数值，最大和是7。&#x20;

**Pascal Triangle Decryption**&#x20;

In order to ensure maximum security, the developers at xyz employ multiple encryption methods to keep user data protected. In one method, numbers are encrypted using a scheme called 'Pascal Triangle". When an array of digits is fed to this system, it sums the adjacent digits. It then takes the rightmost digit (least significant digit) of each luge is repeated addition for the next step. Thus, the number of digits in each step is reduced by 1. This procedige until there are only 2 digits left, and this sequence of 2 digits forms the encrypted number. Given the initial sequence of the digits of numbers, find the encrypted number. You should report a string of digits representing the encrypted number. Function Description Complete the function getEncryptedNumber in the editor below. getEncryptedNumber has the following parameter: int numbers\[n]: the initial sequence of digits Returns string: the encrypted number represented as a string of 2 characters. Constraints 2 <= numbers.length <= 5.10^3 0 <= numbers\[1] ≤ 9 Sample Input For Custom Testing numbers = \[1, 2, 3, 4], n = 4 Sample Output 82 Explanation The encryption occurs as follows: \[1, 2, 3, 4] -> \[3, 5, 7] -> \[8, 2]. Another Input numbers = \[4, 5, 6, 7], n = 4 Sample Output 04 Explanation The encryption occurs as follows: \[4, 5, 6, 7] -> \[9, 1, 3] -> \[0, 4]. 给一组数,相邻两个数相加,如果和大于10,则取个位数,一直到只剩下两个数返回&#x20;

**Group shipment**&#x20;

https://leetcode.com/discuss/int ... /Amazon-orOAorset-7 感觉可以每个最小点可以扩展的最长位置，然后再乘起来。&#x20;

**item rating**&#x20;

连续下降的评分 https://www.1point3acres.com/bbs/thread-885897-1-1.html 假设有一个连续下降数组\[5,4,3,2,1]，那么满足条件的排列数count=5+4+3+2+1=5\*(5+1)/2，所以只要求出原数组中每个连续下降数组的长度，分别计算求和就行&#x20;

**power subarray**&#x20;

https://leetcode.com/discuss/int ... OA-or-SDE-or-90-Min 求所有的min(subarrayPower) \* sum(subarrayPower) 解法1：TC O(n):  2个单调stack找min，然后用prefix sum of prefix sum算sum(subarrayPower)。建议提前练习一下。画个图就很明确了。 感觉是这个题 https://leetcode.com/problems/maximum-subarray-min-product/&#x20;

**Maximum Length of Subarray With Positive Product**&#x20;

https://leetcode.com/discuss/interview-question/1655441/amazon-oa https://leetcode.com/problems/ma ... h-positive-product/&#x20;

**Minimum moves to sort an array**&#x20;

https://leetcode.com/discuss/interview-question/1655441/amazon-oa Given an array containing only 0 and 1 as its elements. We have to sort the array in such a manner that all the ones are grouped together and all the zeros are grouped together. The group of ones can be either at the start of the array or at the end of the array. The constraint while sorting is that every one/zero can be swapped only with its adjacent zero/one. Find the minimum number of moves to sort the array as per the description. Example: input array ={0,1,0,1} Final array = {0,0,1,1} Minimum moves = 1 (1 at index 1 is swapped with 0 at index 2) input array = { 1101} Final array - {1110} Minimum moves = 1 {1 at index 2 is swapped with index 3} I passed all test cases on this one 13/13. I ran a sliding window to check number of swaps if the elements on the left should be 0s before 1s, and at each 0 found by right index, I found the number of swaps needed repeated the same above for the case if the elements on the left should be 1s before 0s, returned the minimum of both operations.&#x20;

Do I have even a miniscule chance of moving forward 解法： 统计0和1个数 分两种情况 计算到左边全0右边1 或者左边1右边0因为相邻的可以自由移动，所以最优解是等于左边所有的1\[0...sum\_zero]到右边所有的0的距离之和\[sum\_zero...l‍‌‌‌‍‌‍‌‌‍‌‌‍‍‌‍‌‌‍‍en]， 或者左边所有的0\[0...sum\_one]到右边所有的1\[sum\_one...len]之和 two pointers 分别求左边1到右边0的dist， 左边0到右边1的dist，每次的dist加上去 然后比较两种情况的最小值&#x20;

类似题 https://leetcode.com/problems/mi ... up-all-1s-together/ https://leetcode.com/contest/wee ... all-1s-together-ii/&#x20;

#### 11.Count unique characters of all subsctrings of a given string&#x20;

https://leetcode.com/problems/co ... -of-a-given-string/&#x20;

#### 气温 计算Change of temperture &#x20;

只记得example 假设三天的气温是【6 -2 5】   第一天 max(\[6],\[6+(-2)+5]) = max(6,9) = 9   第二天  max(\[6+(-2)],\[(-2)+5]]) = max(4,3) = 4   第三天 max(\[6-2+5],\[5]) = max(9,5) = 9   最后return max(9,4,9)=9 就是前后缀数组&#x20;

#### **Prime movie awards**&#x20;

Amazon Prime Video is a subscription video-on-demand over-the-top streaming and rental service. The team at Prime Video is developing a method to divide movies into groups based on the number of awards they have won. A group can consist of any number of movies, but the difference in the number of awards won by any two movies in the group must not exceed k. The movies can be grouped together irrespective of their initial order. Determine the minimum number of groups that can be formed such that each movie is in exactly orly group. Example The numbers of awards per movie are awards = \[1, 5, 4, 6, 8, 9, 2], and the maximum allowed difference is k = 3. One way to divide the movies into the minimum number of groups is: The first group can contain \[2, 1], The maximum difference between awards of any two movies is 1 which does not exceed K. The second group can contain \[5, 4, 6], The maximum difference between awards of any two movies is 2 which does not exceed k. The third group can contain \[8,9]. The maximum difference between awards of any two movies is 1 which does not exceed k. The movies can be divided into a minimum of 3 groups. 是sort完之后greedy吗 就是给一个array of int 和 k， 要求把array分成若干subgroup， 使得每个 subarray 的 max 和 min的diff 不大于k。就是一个sort array，然后loop一边就ok&#x20;

#### Shipment Imbalance&#x20;

https://www.1point3acres.com/bbs/thread-878850-1-1.html https://cybergeeksquad.co/2022/0 ... ance-amazon-oa.html&#x20;

#### Reorder data in log files&#x20;

https://leetcode.com/problems/reorder-data-in-log-files/&#x20;

#### Strength of a password&#x20;

https://www.1point3acres.com/bbs/thread-885221-1-1.html find password Strength for ‍‌‌‌‍‌‍‌‌‍‌‌‍‍‌‍‌‌‍‍a given passwrod. e.g. if password= "good" . Then iterate over all substrings and find the distinct char counts:- g = 1, o = 1, o = 1, d = 1, go = 2, oo = 1, od = 2, goo = 2, ood = 2, good = 3 and at the end add all. here 16 is the password strength and return. Expected output = 16. https://leetcode.com/problems/co ... -of-a-given-string/ 变种&#x20;

#### Ship labels&#x20;

ships millions of packages every day. A large percentage of them are fulfilled by. Amazon, so it is important to minimize shipping costs. It has been found that moving a group of 3 packages to the shipping facility together is most efficient. The shipping process needs to be optimized at a new warehouse. There are the following types of queries or requests: INSERT package id: insert package id in the queue of packages to be shipped SHIP-: ship the group of 3 items that were in the queue earliest i.e. they are returned in the order they entered, Perform q queries and return a list of lists, one for every SHIP - type query. The lists are either; 3 package ID strings in the order they were queued. Or, if there are not enough packages in the queue to fulfill the query, the result is I"N/A"J. Note: ‍‌‍‍‌‌‌‍‍‌‌‍‌‍‌‌‌‍ •: Initially, the queue is empty. •. The list of packages shipped per group should be in the order they were queued. The function performQueries take List\<List<>> of type String as a parameter which contains each query where list.get(i).get(0) = INSERT | SHIP list.get(i).get(1) = shipmentID | - Example Test Case: 5 2 INSERT GT23513413 INSERT TQC2451340 SHIP - INSERT VYP8561991 SHIP Expected result: \[N/A] \[GT23513413, TQC2451340, VYP8561991]&#x20;

#### Maximum deviation&#x20;

https://link.1point3acres.com/?u ... mong-all-substrings 拿两个字母作为key，然后算一下running prefix sum，记录最大值。 Let's have a string: abbbcacbcdce For substring abbb, you have most frequent letter b -> 3 and least frequent letter a -> 1. So the deviation is = most frequent - least frequent = 3 - 1 = 2. You need to look at all the substrings and find the max deviation. Here substring cacbcdc has the max deviation. Frequency is like below: c -> 4, a ->1, b->1, d->1. So max freq - min freq = 4 - 1 = 3. Among all substrings deviation, this is the max. So need to return it. String length is 10^4. So you can't check each substring. Could anyone please help to get the solving technique of this problem? The maximum deviation 就是 difference between the maximum frequency of a character and the minimum frequency of a character. 举个例子, in “abcaba”, "a" 的频率是3; "b"的频率是2; "c" 的频率是1. 所以"a" 是最大频率, which is 3, “c” 是最小频率, which is 1. 最后的deviation of this string is 3-1 = 2. 然后这题问的是在所有的substring里，最大的deviation是多少。&#x20;

#### AWS power consumption&#x20;

https://leetcode.com/discuss/gen ... D%E2%80%8Damazon-oa Question on AWS power consumption, given BootingPower, processingPower, powerMax. For maximum utilization, the data center wishes to group these processors into clusters. Clusters can only be formed of processors located adjacent to each other. For example, processors 2,3,4,5 can form a cluster, but 1,3,4 cannot. cluster of k processors defined as (i, i+1,...., i+k-1) Net power consumption = maximum booting power among the k processors + (sum of processing power of processors)\*k. A cluster is said to be sustainable if it's net power consumption does not exceed a given threshold value powerMax. Example: bootingPower = \[3,6,1,3,4] processingPower = \[2,1,3,4,5] powerMax = 25 If k = 2, any adjacent pair can be choosen. The highest usage is the pair \[4,5] with net power consumption 4 + (4 + 5)2 = 22. Next, try k = 3. Group the first 3 processors together as: Here, Max booting power = max(3,6,1) Sum of processing power = 2 + 1+ 3 = 6 Net power consumption = 6 + 63 = 24 <= powerMax Thus, k = 3 is a sustainable cluster. Example: bootingPower = \[8,8,10,9,2] processingPower = \[4,1,4,5,3] powerMax = 33 If k = 2, consisting of first 2 processors. Net power consumption = max(8,8) + (4+1)\*2 = 18 <= 33 (powerMax) Thus, k = 2 is a sustainable cluster. Example: bootingPower = \[11,12,19] processingPower = \[10,8,7] powerMax = 6 k = 0, not possible to form any sustainable clusters. 解法见链接：sliding window 维持window内power不超过max allow power + 单调栈队列维持window内max power&#x20;

#### Pick item Strict decreasing&#x20;

https://www.1point3acres.com/bbs/thread-886372-1-1.html https://www.1point3acres.com/bbs/thread-874524-1-1.html 链接有讨论，贪心n^2可以pass，link里有O(n)解。&#x20;

#### Next non-palindrome string&#x20;

https://www.1point3acres.com/bbs/thread-885430-1-1.html&#x20;

#### Delivery day&#x20;

https://www.1point3acres.com/bbs/thread-885430-1-1.html&#x20;

#### MEX array of array&#x20;

https://www.1point3acres.com/bbs/thread-884439-1-1.html
