93. Restore IP Addresses

A valid IP address consists of exactly four integers separated by single dots. Each integer is between 0 and 255 (inclusive) and cannot have leading zeros.

    For example, "0.1.2.201" and "192.168.1.1" are valid IP addresses, but "0.011.255.245", "192.168.1.312" and "192.168@1.1" are invalid IP addresses.

Given a string s containing only digits, return all possible valid IP addresses that can be formed by inserting dots into s. You are not allowed to reorder or remove any digits in s.


```

func restoreIpAddresses(s string) []string {
	res := make([]string, 0)
	backtrack(s, &res, nil)
	return res
}

func backtrack(s string, res *[]string, cur []string) {
	if len(s) == 0 && len(cur) == 4 {
		*res = append(*res, strings.Join(cur, "."))
		return
	}

	if len(cur) > 4 {
		return
	}

	for i := 1; i <= 3 && i <= len(s); i++ {
		if isValid(s[0:i]) {
			backtrack(s[i:], res, append(cur, s[0:i]))
		}
	}
}

func isValid(s string) bool {
	num, _ := strconv.Atoi(s)
	if num > 255 {
		return false
	}
    
    if strings.HasPrefix(s, "0") && len(s) != 1 {
        return false
    }
    
    return true
}
```