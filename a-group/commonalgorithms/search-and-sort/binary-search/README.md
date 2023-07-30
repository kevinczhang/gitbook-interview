# Binary search

## **Search for a target**

```java
int binarySearch(int[] nums, int target) {
    int left = 0; 
    int right = nums.length - 1; // 注意

    while(left <= right) {
        int mid = left + (right - left) / 2;
        if(nums[mid] == target)
            return mid; 
        else if (nums[mid] < target)
            left = mid + 1; // 注意
        else if (nums[mid] > target)
            right = mid - 1; // 注意
    }
    return -1;
}

```

**Distinguishing Syntax:**

* 因为我们初始化 right = nums.length - 1 所以决定了我们的「搜索区间」是 \[left, right] 所以决定了 while (left <= right) 同时也决定了 left = mid+1 和 right = mid-1
* 因为我们只需找到一个 target 的索引即可 所以当 nums\[mid] == target 时可以立即返回

## **Search left bound**

```java
int left_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    // 搜索区间为 [left, right]
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            // 搜索区间变为 [mid+1, right]
            left = mid + 1;
        } else if (nums[mid] > target) {
            // 搜索区间变为 [left, mid-1]
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 收缩右侧边界
            right = mid - 1;
        }
    }
    // 判断 target 是否存在于 nums 中
    // 此时 target 比所有数都大，返回 -1
    if (left == nums.length) return -1;
    // 判断一下 nums[left] 是不是 target
    return nums[left] == target ? left : -1;
}

```

**Distinguishing Syntax:**

* 因为我们初始化 right = nums.length 所以决定了我们的「搜索区间」是 \[left, right) 所以决定了 while (left < right) 同时也决定了 left = mid + 1 和 right = mid
* 因为我们需找到 target 的最左侧索引 所以当 nums\[mid] == target 时不要立即返回 而要收紧右侧边界以锁定左侧边界

## **Search right bound**

```java
int right_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 这里改成收缩左侧边界即可
            left = mid + 1;
        }
    }
    // 最后改成返回 left - 1
    if (left - 1 < 0) return -1;
    return nums[left - 1] == target ? (left - 1) : -1;
}

```

**Distinguishing Syntax:**

* 因为我们初始化 right = nums.length 所以决定了我们的「搜索区间」是 \[left, right) 所以决定了 while (left < right) 同时也决定了 left = mid + 1 和 right = mid
* 因为我们需找到 target 的最右侧索引 所以当 nums\[mid] == target 时不要立即返回 而要收紧左侧边界以锁定右侧边界
* 又因为收紧左侧边界时必须 left = mid + 1 所以最后无论返回 left 还是 right，必须减一
