# OA2022



## === 如果下面有链接打不开，可以用google cache打开 https://cachedview.com/

## OA dp April/18，SDE2， 90 mins 2 codings，其余部分不限时。 code1: item rating，给一个数组ratings，e.g \[5,4] 找到连续严格下降(rating = rating\[i+1] -1)subarray的个数。这个eg的答案是3，\[5], \[4], \[5,4].解法：TC O(n), 用sliding widnow保持一个连续下降的rating，遇到使它不连续的时候，就count += len \* (len+1) /2, 然后清空window的rating。这个同学有完整code1的贴图和最优解 code 2: power subarray，求所有的min(subarrayPower) \* sum(subarrayPower) 这个同学有完整贴图 解法1：TC O(n):  2个单调stack找min，然后用prefix sum of prefix sum算sum(subarrayPower)。建议提前练习一下。画个图就很明确了。 解法2:  详见leetcode讨论 感受是：我是不李姐为什么亚麻欧埃怎么变得这么难了，不仅包变小了，题还hard+。。。subarray走火入魔。。

3月-4月code2总结， 按照频率从大到小大概排了一下。code1相对比较简单应该没太大问题就没列出来了，OA时建议多留些时间给code2。

1. power subarray （楼主遇到的题）
2. password strength 链接里的解法可pass 3.Segment no more than k， 解法 slidng widnow+min/max queue
3. \[url=http://webcache.googleusercontent.com/search?q=cache:https://leetcode.com/discuss/int ... -OA\&strip=1\&vwsrc=0]student rank\[/url] : 解法链接里有答案
4. Max deviation among all substrings： 链接里有答案，解法 O(2&#x36;_&#x32;&#x36;_&#x6E;), 拿两个字母作为key，然后算一下running prefix sum，记录最大值。
5. AWS power consumption： 解法见链接：sliding window 维持window内power不超过max allow power + 单调栈队列维持window内max power
6. shipment imbalance ：解法见链接。4 个单调栈，算某个value可以作为subarray中的minValue和maxValue的可能性个数，类似刷题网扒尔扒。
7. pick item strict decreasing， 链接有讨论，贪心n^2可以pass，link里有O(n)解。
8. next non-palindrome string : 链接有讨论，只想到暴力解，从右往左找到第一个非“z“的char加1。把后面全改成“a”得到新str。O(n)遍历新的str看是否含有长度2个/3个的palindrome
9. MEX array of array链接有讨论，只想到暴力解，用一个running treeSet维持当前subarray缺省的number，遍历所有的subarray，某subarray的MEX就是treeSet\[0]。 ======
