# [2171. 拿出最少数目的魔法豆](https://leetcode.cn/problems/removing-minimum-number-of-magic-beans)

[English Version](/solution/2100-2199/2171.Removing%20Minimum%20Number%20of%20Magic%20Beans/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给定一个 <strong>正整数&nbsp;</strong>数组&nbsp;<code>beans</code>&nbsp;，其中每个整数表示一个袋子里装的魔法豆的数目。</p>

<p>请你从每个袋子中&nbsp;<strong>拿出</strong>&nbsp;一些豆子（也可以<strong>&nbsp;不拿出</strong>），使得剩下的 <strong>非空</strong> 袋子中（即 <strong>至少还有一颗</strong>&nbsp;魔法豆的袋子）魔法豆的数目&nbsp;<strong>相等</strong>。一旦把魔法豆从袋子中取出，你不能再将它放到任何袋子中。</p>

<p>请返回你需要拿出魔法豆的 <strong>最少数目</strong>。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<b>输入：</b>beans = [4,1,6,5]
<b>输出：</b>4
<b>解释：</b>
- 我们从有 1 个魔法豆的袋子中拿出 1 颗魔法豆。
  剩下袋子中魔法豆的数目为：[4,<u><strong>0</strong></u>,6,5]
- 然后我们从有 6 个魔法豆的袋子中拿出 2 个魔法豆。
  剩下袋子中魔法豆的数目为：[4,0,<u><strong>4</strong></u>,5]
- 然后我们从有 5 个魔法豆的袋子中拿出 1 个魔法豆。
  剩下袋子中魔法豆的数目为：[4,0,4,<u><strong>4</strong></u>]
总共拿出了 1 + 2 + 1 = 4 个魔法豆，剩下非空袋子中魔法豆的数目相等。
没有比取出 4 个魔法豆更少的方案。
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<b>输入：</b>beans = [2,10,3,2]
<b>输出：</b>7
<strong>解释：</strong>
- 我们从有 2 个魔法豆的其中一个袋子中拿出 2 个魔法豆。
  剩下袋子中魔法豆的数目为：[<u><strong>0</strong></u>,10,3,2]
- 然后我们从另一个有 2 个魔法豆的袋子中拿出 2 个魔法豆。
  剩下袋子中魔法豆的数目为：[0,10,3,<u><strong>0</strong></u>]
- 然后我们从有 3 个魔法豆的袋子中拿出 3 个魔法豆。
  剩下袋子中魔法豆的数目为：[0,10,<u><strong>0</strong></u>,0]
总共拿出了 2 + 2 + 3 = 7 个魔法豆，剩下非空袋子中魔法豆的数目相等。
没有比取出 7 个魔法豆更少的方案。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= beans.length &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= beans[i] &lt;= 10<sup>5</sup></code></li>
</ul>

## 解法

### 方法一：排序求和

<!-- tabs:start -->

```python
class Solution:
    def minimumRemoval(self, beans: List[int]) -> int:
        beans.sort()
        ans = s = sum(beans)
        n = len(beans)
        for i, v in enumerate(beans):
            ans = min(ans, s - v * (n - i))
        return ans
```

```java
class Solution {
    public long minimumRemoval(int[] beans) {
        Arrays.sort(beans);
        long s = 0;
        for (int v : beans) {
            s += v;
        }
        long ans = s;
        int n = beans.length;
        for (int i = 0; i < n; ++i) {
            ans = Math.min(ans, s - (long) beans[i] * (n - i));
        }
        return ans;
    }
}
```

```cpp
class Solution {
public:
    long long minimumRemoval(vector<int>& beans) {
        sort(beans.begin(), beans.end());
        long long s = accumulate(beans.begin(), beans.end(), 0ll);
        long long ans = s;
        int n = beans.size();
        for (int i = 0; i < n; ++i) ans = min(ans, s - 1ll * beans[i] * (n - i));
        return ans;
    }
};
```

```go
func minimumRemoval(beans []int) int64 {
	sort.Ints(beans)
	s := 0
	for _, v := range beans {
		s += v
	}
	ans := s
	n := len(beans)
	for i, v := range beans {
		ans = min(ans, s-v*(n-i))
	}
	return int64(ans)
}
```

```ts
function minimumRemoval(beans: number[]): number {
    const n = beans.length;
    let sum = beans.reduce((a, c) => a + c, 0);
    beans.sort((a, b) => a - b);
    let ans = sum;
    for (let i = 0; i < n; i++) {
        let num = beans[i];
        ans = Math.min(sum - num * (n - i), ans);
    }
    return ans;
}
```

<!-- tabs:end -->

<!-- end -->
