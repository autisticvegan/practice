## Max Number of Books You Can Take

- lc 2355




`
non-stack approach
func maximumBooks(books []int) int64 {

    prev := 0
    count := 0
    index := 0
    sequence := make(map[int]int64)

    for i, c := range books  {
        if c <= prev  {
            sequence[index] = int64(count)
            count = c
            index = i 
        } else {
            count += c
        }

        prev = c
    }

    sequence[index] = int64(count)

    var total int64 = 0
    for i, sum := range sequence {
        min := books[i]
        for j:=i-1;0<=j;j-- {
           take := books[j] 
           if take >= min {
               take = min - 1
           }
           if take > 0 {
               sum += int64(take)
               min = take
           } else {
               break
           }
        }
        if sum > total {
            total = sum
        }
    }
    
    return total
`

`
stack approach
    def maximumBooks(self, books: List[int]) -> int:
        res = 0
        stack = []
        for i in range(len(books)):
            while stack and books[i]<=books[stack[-1][0]]+(i-stack[-1][0]):
                stack.pop()
            prev_g_end,prev_g_res = stack[-1] if stack else [-1,0]
            h = min(i-prev_g_end,books[i])
            l1,l2 = books[i],books[i]-h+1
            cur = prev_g_res+(l1+l2)*h//2
            stack.append([i,cur])
            res = max(res,cur)
        return res
`