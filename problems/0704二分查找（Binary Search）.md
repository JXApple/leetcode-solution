题目描述：[704. 二分查找](https://leetcode-cn.com/problems/binary-search/) 难度简单

给定一个 `n` 个元素有序的（升序）整型数组 `nums` 和一个目标值 `target`  ，写一个函数搜索 `nums` 中的 `target`，如果目标值存在返回下标，否则返回 `-1`。

**示例 1:**

```
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
```

**示例 2:**

```
输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```

**提示：**

1. 你可以假设 `nums` 中的所有元素是不重复的。
2. `n` 将在 `[1, 10000]`之间。
3. `nums` 的每个元素都将在 `[-9999, 9999]`之间。

解法一：暴力解决（直接循环整个数组，判断循环数组的值与目标值是否相等，相等则直接return下标，否则返回-1）

```typescript
function search(nums: number[], target: number): number {
    for(let i = 0,len = nums.length;i<len;i++) {
        if(nums[i] == target) {
            return i;
        }
    }
    return -1
};
```

解法二：二分查找（使用二分查找**前提条件**：**升序且无重复数字**）用二进制运算符速度真的快，虽然可读性不高

​      写法一:

```typescript
function search(nums: number[], target: number): number {
    let start:number = 0, end:number = nums.length;
    //左闭右开[start,end)
    while(start < end) {
        let mid = start + ((end - start) >> 1); //防溢出，equal(start+end)/2
        if(nums[mid] < target) {
            start = mid + 1;
        }else if(nums[mid] > target){
            end = mid;
        }else {
            return mid;
        }
    }
    return -1
};
```

​     写法二：

```typescript
function search(nums: number[], target: number): number {
    let start:number = 0, end:number = nums.length - 1;
    //左闭右闭[start,end]
    while(start <= end) {
        let mid = start + ((end - start) >> 1); //防溢出，equal(start+end)/2
        if(nums[mid] < target) {
            start = mid + 1;
        }else if(nums[mid] > target){
            end = mid - 1;
        }else {
            return mid;
        }
    }
    return -1;
};
```

