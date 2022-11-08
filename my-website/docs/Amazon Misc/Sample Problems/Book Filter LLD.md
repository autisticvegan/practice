
LLD in Go = roflmao (Amazon's example was a bookfilter that inherited)

So instead of a bookfilter example we are going to look at enums!

```
type Season int64

const (
	Summer Season = 0
	Autumn        = 1
	Winter        = 2
	Spring        = 3
)

const (
	Summer int = 0
	Autumn     = 1
	Winter     = 2
	Spring     = 3
)

// string mapping
const (
	Summer string = "summer"
	Autumn        = "autumn"
	Winter        = "winter"
	Spring        = "spring"
)


```