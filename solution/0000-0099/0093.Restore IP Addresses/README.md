# [93. 复原 IP 地址](https://leetcode.cn/problems/restore-ip-addresses)

[English Version](/solution/0000-0099/0093.Restore%20IP%20Addresses/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p><strong>有效 IP 地址</strong> 正好由四个整数（每个整数位于 <code>0</code> 到 <code>255</code> 之间组成，且不能含有前导 <code>0</code>），整数之间用 <code>'.'</code> 分隔。</p>

<ul>
	<li>例如：<code>"0.1.2.201"</code> 和<code> "192.168.1.1"</code> 是 <strong>有效</strong> IP 地址，但是 <code>"0.011.255.245"</code>、<code>"192.168.1.312"</code> 和 <code>"192.168@1.1"</code> 是 <strong>无效</strong> IP 地址。</li>
</ul>

<p>给定一个只包含数字的字符串 <code>s</code> ，用以表示一个 IP 地址，返回所有可能的<strong>有效 IP 地址</strong>，这些地址可以通过在 <code>s</code> 中插入&nbsp;<code>'.'</code> 来形成。你 <strong>不能</strong>&nbsp;重新排序或删除 <code>s</code> 中的任何数字。你可以按 <strong>任何</strong> 顺序返回答案。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre>
<strong>输入：</strong>s = "25525511135"
<strong>输出：</strong>["255.255.11.135","255.255.111.35"]
</pre>

<p><strong>示例 2：</strong></p>

<pre>
<strong>输入：</strong>s = "0000"
<strong>输出：</strong>["0.0.0.0"]
</pre>

<p><strong>示例 3：</strong></p>

<pre>
<strong>输入：</strong>s = "101023"
<strong>输出：</strong>["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 20</code></li>
	<li><code>s</code> 仅由数字组成</li>
</ul>

## 解法

### 方法一：DFS

我们定义一个函数 $dfs(i)$，表示从字符串 $s$ 的第 $i$ 位开始，搜索能够组成的 IP 地址列表。

函数 $dfs(i)$ 的执行步骤如下：

如果 $i$ 大于等于字符串 $s$ 的长度，说明已经完成了四段 IP 地址的拼接，判断是否满足四段 IP 地址的要求，如果满足则将当前 $IP$ 加入答案。

如果 $i$ 小于字符串 $s$ 的长度，此时还需要拼接 $IP$ 地址的一段，此时需要确定这一段 $IP$ 地址的值。如果该值大于 $255$，或者当前位置 $i$ 为 $0$ 且 $i$ 之后的若干位的数值大于 $0$，则说明不满足要求，直接返回。否则，将其加入 $IP$ 地址列表，并继续搜索下一段 $IP$ 地址。

时间复杂度 $O(n \times 3^4)$，空间复杂度 $O(n)$。其中 $n$ 为字符串 $s$ 的长度。

<!-- tabs:start -->

```python
class Solution:
    def restoreIpAddresses(self, s: str) -> List[str]:
        def check(i: int, j: int) -> int:
            if s[i] == "0" and i != j:
                return False
            return 0 <= int(s[i : j + 1]) <= 255

        def dfs(i: int):
            if i >= n and len(t) == 4:
                ans.append(".".join(t))
                return
            if i >= n or len(t) >= 4:
                return
            for j in range(i, min(i + 3, n)):
                if check(i, j):
                    t.append(s[i : j + 1])
                    dfs(j + 1)
                    t.pop()

        n = len(s)
        ans = []
        t = []
        dfs(0)
        return ans
```

```java
class Solution {
    private int n;
    private String s;
    private List<String> ans = new ArrayList<>();
    private List<String> t = new ArrayList<>();

    public List<String> restoreIpAddresses(String s) {
        n = s.length();
        this.s = s;
        dfs(0);
        return ans;
    }

    private void dfs(int i) {
        if (i >= n && t.size() == 4) {
            ans.add(String.join(".", t));
            return;
        }
        if (i >= n || t.size() >= 4) {
            return;
        }
        int x = 0;
        for (int j = i; j < Math.min(i + 3, n); ++j) {
            x = x * 10 + s.charAt(j) - '0';
            if (x > 255 || (s.charAt(i) == '0' && i != j)) {
                break;
            }
            t.add(s.substring(i, j + 1));
            dfs(j + 1);
            t.remove(t.size() - 1);
        }
    }
}
```

```cpp
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        int n = s.size();
        vector<string> ans;
        vector<string> t;
        function<void(int)> dfs = [&](int i) {
            if (i >= n && t.size() == 4) {
                ans.push_back(t[0] + "." + t[1] + "." + t[2] + "." + t[3]);
                return;
            }
            if (i >= n || t.size() >= 4) {
                return;
            }
            int x = 0;
            for (int j = i; j < min(n, i + 3); ++j) {
                x = x * 10 + s[j] - '0';
                if (x > 255 || (j > i && s[i] == '0')) {
                    break;
                }
                t.push_back(s.substr(i, j - i + 1));
                dfs(j + 1);
                t.pop_back();
            }
        };
        dfs(0);
        return ans;
    }
};
```

```go
func restoreIpAddresses(s string) (ans []string) {
	n := len(s)
	t := []string{}
	var dfs func(int)
	dfs = func(i int) {
		if i >= n && len(t) == 4 {
			ans = append(ans, strings.Join(t, "."))
			return
		}
		if i >= n || len(t) == 4 {
			return
		}
		x := 0
		for j := i; j < i+3 && j < n; j++ {
			x = x*10 + int(s[j]-'0')
			if x > 255 || (j > i && s[i] == '0') {
				break
			}
			t = append(t, s[i:j+1])
			dfs(j + 1)
			t = t[:len(t)-1]
		}
	}
	dfs(0)
	return
}
```

```ts
function restoreIpAddresses(s: string): string[] {
    const n = s.length;
    const ans: string[] = [];
    const t: string[] = [];
    const dfs = (i: number): void => {
        if (i >= n && t.length === 4) {
            ans.push(t.join('.'));
            return;
        }
        if (i >= n || t.length === 4) {
            return;
        }
        let x = 0;
        for (let j = i; j < i + 3 && j < n; ++j) {
            x = x * 10 + s[j].charCodeAt(0) - '0'.charCodeAt(0);
            if (x > 255 || (j > i && s[i] === '0')) {
                break;
            }
            t.push(x.toString());
            dfs(j + 1);
            t.pop();
        }
    };
    dfs(0);
    return ans;
}
```

```cs
public class Solution {
    private IList<string> ans = new List<string>();
    private IList<string> t = new List<string>();
    private int n;
    private string s;

    public IList<string> RestoreIpAddresses(string s) {
        n = s.Length;
        this.s = s;
        dfs(0);
        return ans;
    }

    private void dfs(int i) {
        if (i >= n && t.Count == 4) {
            ans.Add(string.Join(".", t));
            return;
        }
        if (i >= n || t.Count == 4) {
            return;
        }
        int x = 0;
        for (int j = i; j < i + 3 && j < n; ++j) {
            x = x * 10 + (s[j] - '0');
            if (x > 255 || (j > i && s[i] == '0')) {
                break;
            }
            t.Add(x.ToString());
            dfs(j + 1);
            t.RemoveAt(t.Count - 1);
        }
    }
}
```

<!-- tabs:end -->

<!-- end -->
