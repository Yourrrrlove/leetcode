# [1920. 基于排列构建数组](https://leetcode.cn/problems/build-array-from-permutation)

[English Version](/solution/1900-1999/1920.Build%20Array%20from%20Permutation/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给你一个 <strong>从 0 开始的排列</strong> <code>nums</code>（<strong>下标也从 0 开始</strong>）。请你构建一个 <strong>同样长度</strong> 的数组 <code>ans</code> ，其中，对于每个 <code>i</code>（<code>0 &lt;= i &lt; nums.length</code>），都满足 <code>ans[i] = nums[nums[i]]</code> 。返回构建好的数组 <code>ans</code> 。</p>

<p><strong>从 0 开始的排列</strong> <code>nums</code> 是一个由 <code>0</code> 到 <code>nums.length - 1</code>（<code>0</code> 和 <code>nums.length - 1</code> 也包含在内）的不同整数组成的数组。</p>

<p> </p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>nums = [0,2,1,5,3,4]
<strong>输出：</strong>[0,1,2,4,5,3]<strong>
解释：</strong>数组 ans 构建如下：
ans = [nums[nums[0]], nums[nums[1]], nums[nums[2]], nums[nums[3]], nums[nums[4]], nums[nums[5]]]
    = [nums[0], nums[2], nums[1], nums[5], nums[3], nums[4]]
    = [0,1,2,4,5,3]</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>nums = [5,0,1,2,3,4]
<strong>输出：</strong>[4,5,0,1,2,3]
<strong>解释：</strong>数组 ans 构建如下：
ans = [nums[nums[0]], nums[nums[1]], nums[nums[2]], nums[nums[3]], nums[nums[4]], nums[nums[5]]]
    = [nums[5], nums[0], nums[1], nums[2], nums[3], nums[4]]
    = [4,5,0,1,2,3]</pre>

<p> </p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 1000</code></li>
	<li><code>0 &lt;= nums[i] &lt; nums.length</code></li>
	<li><code>nums</code> 中的元素 <strong>互不相同</strong></li>
</ul>

## 解法

### 方法一

<!-- tabs:start -->

```python
class Solution:
    def buildArray(self, nums: List[int]) -> List[int]:
        return [nums[num] for num in nums]
```

```java
class Solution {
    public int[] buildArray(int[] nums) {
        int[] ans = new int[nums.length];
        for (int i = 0; i < nums.length; ++i) {
            ans[i] = nums[nums[i]];
        }
        return ans;
    }
}
```

```cpp
class Solution {
public:
    vector<int> buildArray(vector<int>& nums) {
        vector<int> ans;
        for (int& num : nums) {
            ans.push_back(nums[num]);
        }
        return ans;
    }
};
```

```go
func buildArray(nums []int) []int {
	ans := make([]int, len(nums))
	for i, num := range nums {
		ans[i] = nums[num]
	}
	return ans
}
```

```ts
function buildArray(nums: number[]): number[] {
    return nums.map(v => nums[v]);
}
```

```rust
impl Solution {
    pub fn build_array(nums: Vec<i32>) -> Vec<i32> {
        nums.iter()
            .map(|&v| nums[v as usize])
            .collect()
    }
}
```

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var buildArray = function (nums) {
    let ans = [];
    for (let i = 0; i < nums.length; ++i) {
        ans[i] = nums[nums[i]];
    }
    return ans;
};
```

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* buildArray(int* nums, int numsSize, int* returnSize) {
    int* ans = malloc(sizeof(int) * numsSize);
    for (int i = 0; i < numsSize; i++) {
        ans[i] = nums[nums[i]];
    }
    *returnSize = numsSize;
    return ans;
}
```

<!-- tabs:end -->

<!-- end -->
