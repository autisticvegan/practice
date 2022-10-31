2281. Sum of Total Strength of Wizards

You are given a 0-indexed integer array strength, where strength[i] denotes the strength of the ith wizard. For a contiguous group of wizards (i.e. the wizards' strengths form a subarray of strength), the total strength is defined as the product of the following two values:

    The strength of the weakest wizard in the group.
    The total of all the individual strengths of the wizards in the group.

Return the sum of the total strengths of all contiguous groups of wizards. Since the answer may be very large, return it modulo 109 + 7.


prefix sum of prefix sum

```
type stack []int

func (s *stack) pop() int {
	var (
		i = len(*s) - 1
		x = (*s)[i]
	)
	*s = (*s)[:i]
	return x
}
func (s stack) top() int { return s[len(s)-1] }
func (s *stack) push(x int) { *s = append(*s, x) }
func (s stack) empty_unused() bool { return len(s)  == 0 }

func totalStrength(strength []int) int {
	var (
		mod = int64(1000000007)
		res int64
		S   = stack{0}
		p   int64
		P   = []int64{0}
		A   = make([]int, len(strength)+2)
		n   = len(A)
	)
	copy(A[1:n-1], strength)

	for r := 0; r < n; r++ {
		p += int64(A[r])
		P = append(P, (P[len(P)-1]+p)%mod)
		for A[S.top()] > A[r] {
			i := S.pop()
			l := S.top()
			res = (res + int64(A[i])*((int64(i-l)*(P[r]-P[i])-int64(r-i)*(P[i]-P[l]))%mod+mod)) % mod
		}
		S.push(r)
	}
	return int(res)
}
```

```
int totalStrength(vector<int>& s) {
    long long res = 0, sz = s.size(), mod = 1000000007;
    vector<int> st; // mono-increasing stack.
    vector<long long> pps(s.size() + 1);
    partial_sum(begin(s), end(s), begin(pps) + 1, [&](int s, int n){ return (s + n) % mod; });
    partial_sum(begin(pps), end(pps), begin(pps));
    for (int r = 0; r <= sz; ++r) {
        while(!st.empty() && (r == sz || s[st.back()] >= s[r])) {
            long long i = st.back(); st.pop_back();
            long long l = st.empty() ? -1 : st.back();
            res = (res + (mod + (pps[r] - pps[i]) * (i - l) % mod - (pps[i] - pps[max(0LL, l)]) * (r - i) % mod) * s[i]) % mod;
        }
        st.push_back(r);
    }
    return res;
}
```




[Related - Largest Rectangle in Histogram](./Largest Rect in Histo.md)
