
convertBST
digitcount
remove anagrams
something about removing parens
working hours and tasks
text cursor
getfancyVal
WiggleSort
```

//copied
impl Solution {
    pub fn remove_anagrams(words: Vec<String>) -> Vec<String> {
        let mut res = vec![];
        for w in words {
            let n = res.len();
            if n == 0 {
                res.push(w);
                continue
            }
            let tail = &res[n-1];
            let mut ana: Vec<char> = tail.chars().collect();
            ana.sort();
            let mut w_ana = w.chars().collect::<Vec<char>>();
            w_ana.sort();
            if ana != w_ana {
                res.push(w);
            }
        }
        res
    }
}

// For each word, count the number of each letter
// compare it to the previous one
// if it doesn't match, put it in the results
// before starting next iteration in loop, save the curr result
// into the prev result
//
// note - because we are case insensitive we can use an array
// instead of a dict

impl Solution {
    pub fn remove_anagrams(words: Vec<String>) -> Vect<String> {
        let mut res = vec![];
        let mut prev_count_dict = [0; 26];

        for word in words {
            let mut current_letters_count_dict = [0; 26];
            word.bytes().for_each(|b| current_letters_count_dict[(b - b'a') as usize] += 1);

            if prev_count_dict != current_letters_count_dict {
                res.push(word);
            }

            prev_count_dict = current_letters_count_dict;
        }
        res
    }

    // copied
class Solution {
    public:
        vector<string> removeAnagrams(vector<string>& words) {
            for(int i = 1;i<words.size();i++){
                string x = words[i];
                sort(x.begin(),x.end());
                string y = words[i-1];
                sort(y.begin(),y.end());
                if(x == y){
                    words.erase(words.begin() + i);
                    i--;
                }
            }
            return words;
        }
    };

// magic function made by stefanpochmann to split up big and small vs even and odd

// BAD SOLUTION LOL - for real solution go below
int getFancyVal(std::vector<int>& nums, int index) {
    int doubleIndexPlusOne = 2 * i + 1;

    /*
    to see how the section works, do this. AS you can see it just rounds it up to the odd
    std::cout << (1|1) << std::endl;
    std::cout << (0|1) << std::endl;
    std::cout << (2|1) << std::endl;
    std::cout << (3|1) << std::endl
        std::cout << (4|1) << std::endl;
    std::cout << (5|1) << std::endl;
    */

    int section = nums.size()|1;
    return nums[doubleIndexPlusOne % section];
}

void wiggleSort(std::vector<int>& nums) {
    int size = nums.size();

    auto midPointer = nums.begin() + size / 2;
    std::nth_element(nums.begin(), midPointer, nums.end());
    int midPointNum = *midPointer;

    int front = 0;
    int back = size - 1;
    int swapPoint = 0;

    while(front <= back) {
        if (getFancyVal(front) > midPointNum)
            std::swap(getFancyVal(swapPoint++), getFancyVal(front++));
        else if (getFancyVal(front) < midPointNum)
            std::swap(getFancyVal(swapPoint++), getFancyVal(back--));
        else
            front++;
    }
}


// problems still to do:
// trapping rainwater
// friendship circles
// wigglesort 1
// all neetcode
// everything from uber
// everything from stripe
// everything from pinterest
// everything from airbnb
// everything from robinhood
// everything from linkedin
// everything from facebook
// everything from google
// everything from twitter
// everything from amazon
// everything from databricks
// everything from snowflake
// everything from quora
// everything from coinbase
// everything from github
// citadel
// 2sigma
// optiver
// nuro
// cruise
// convoy
// instacart
// plaid
// HRT
// DRW
// PDT partners
// square
// chime
// amplitude
// dropbox
// snap
// figma
// scaleai
// airtable
// bytedance
// argo
// asana
// dfinity
// ramp ? (lol)
// brex?



/*
class Solution {
public:
    
    int getFancyVal(std::vector<int>& nums, int index) {
    int doubleIndexPlusOne = 2 * index + 1;
    int section = nums.size()|1;
    return doubleIndexPlusOne % section;
}
    
    void wiggleSort(vector<int>& nums) {
            int size = nums.size();

    auto midPointer = nums.begin() + size / 2;
    std::nth_element(nums.begin(), midPointer, nums.end());
    int midPointNum = *midPointer;

    int front = 0;
    int back = size - 1;
    int swapPoint = 0;

    while(front <= back) {
        if (nums[getFancyVal(nums, front)] > midPointNum)
            std::swap(nums[getFancyVal(nums, swapPoint++)], nums[getFancyVal(nums, front++)]);
        else if (nums[getFancyVal(nums, front)] < midPointNum)
            std::swap(nums[getFancyVal(nums, front)], nums[getFancyVal(nums, back--)]);
        else
            front++;
    }
    }
};
*/


// copy the array size (dp memo)
// go backwards through array (we are iterating indices)

// while stack is not empty and current num > num on top
// dp[i] = max(dp[i] + 1, dp[top])
// pop

// every iteration push the index into the stack
// every iteration check for max
 
class Solution {
    public:
    int totalSteps(std::vector<int>& nums) {

        std::vector<int> dp(nums.size());
        std::stack<int> maxStack;
        int numSteps = 0;

        for(int i = nums.size() - 1;  i >= 0; i--) {
            while(!maxStack.empty() && nums[i] > nums[maxStack.top()]) {
                dp[i] = std::max(dp[maxStack.top()], dp[i] + 1);
                maxStack.pop();
            }
            maxStack.push(i);
            numSteps = std::max(numSteps, dp[i]);
        }


        return numSteps;
    }
}

string before, after;
void addText(string text) {
    before.insert(end(before), begin(text), end(text));
}
int deleteText(int k) {
    k = min(k, (int)before.size());
    before.resize(before.size() - k);
    return k;
}
string cursorLeft(int k) {
    while(k-- && !before.empty()) {
        after.push_back(before.back());
        before.pop_back();
    }
    return before.substr(before.size() - min((int)before.size(), 10));
}
string cursorRight(int k) {
    while(k-- && !after.empty()) {
        before.push_back(after.back());
        after.pop_back();
    }
    return before.substr(before.size() - min((int)before.size(), 10));
}

int main()
{
    addText("hello");
    addText("world");
    std::cout << "before is " << before << std::endl;
    std::cout << "after is " << after << std::endl;
    std::cout << "moving cursor left 1" << std::endl;
    std::string curr = cursorLeft(1);
    std::cout << curr << std::endl;
    std::cout << "before is " << before << std::endl;
    std::cout << "after is " << after << std::endl;
    std::cout << "moving cursor right 5" << std::endl;
    curr = cursorRight(5);
    std::cout << curr << std::endl;
    
    std::cout << "before is " << before << std::endl;
    std::cout << "after is " << after << std::endl;
    std::cout << "deleting 2 " << std::endl;
    deleteText(2);
    std::cout << "before is " << before << std::endl;
    std::cout << "after is " << after << std::endl;
}


var currentDays []int
var state2daysSoFar map[string]int
var workHours int
var lengthOfTasks int
var theTasks []int

func recursive(index int) int {
    
    if index >= lengthOfTasks {
        return 0
    }
    
    stateStr := ""
    for _, c := range currentDays {
        stateStr += string(c)
    }
    state := string(index) + stateStr
    
    if val, ok := state2daysSoFar[state]; ok {
        return val
    }
    
    currentDays = append(currentDays, theTasks[index])
    onePlusSolve := 1 + recursive(index + 1)
    currentDays = currentDays[:len(currentDays) - 1]
    
    for i, _ := range currentDays {
        if currentDays[i] + theTasks[index] <= workHours {
            currentDays[i] += theTasks[index]
            
            newVal := recursive(index + 1)
            if newVal < onePlusSolve {
                onePlusSolve = newVal
            }
            
            currentDays[i] -= theTasks[index]
        }
    } 
    
    
    state2daysSoFar[state] = onePlusSolve
    return onePlusSolve
}

func solution(workingHours int, tasks []int) int {
    state2daysSoFar = make(map[string]int)
    lengthOfTasks = len(tasks)
    workHours = workingHours
    theTasks = tasks
    for _, t := range tasks {
        if t > workingHours {
            return -1
        }
    }
    // position, tasks, sessiontime
    return recursive(0)    
}

// find first parens, find last parens
// reverse mid so on and so forth
// 

// hyupo.ueid(xyz)aonheu
//           ^   ^
// 
func reverse(str string, openParenthesesIndex int, closeParenthesesIndex int) string {
 
    var res string
    for i := closeParenthesesIndex - 1; i >= openParenthesesIndex + 1; i-- {
        fmt.Println("printing inside reverse, ")
        fmt.Println(string(str[i]))
        res = res + string(str[i])
    }
    return res
}

func solution(inputString string) string {

     var stack []int
     
     for i, c := range inputString {
         if c != ')' && c != '(' {
            continue   
         } else if c == '(' {
            stack = append(stack, i)    
         } else {
               // case of c being )
               lookBack := stack[len(stack)-1]
               stack = stack[:len(stack)-1]
               
               p1 := inputString[:lookBack+1]
               p2 := reverse(inputString, lookBack, i)
               p3 := inputString[i:]
                fmt.Println("p1 is " + p1)
                fmt.Println(p2)
                fmt.Println(p3)
               inputString =  p1 + p2 + p3
         }
     }
     
     fmt.Println(inputString)
     parensRemoved := ""
     for _, c := range inputString {
         if c != '(' && c != ')' {
             parensRemoved = parensRemoved + string(c)
         }
     }
     
     return parensRemoved
}


func digitCount(in int) int {
    count := 0
    for {
        if in == 0 {
            break
        }
        count++
        in /= 10
    }
    
    return count
}


func solution(a []int) int64 {

res := int64(0)
num2DigitCount := make(map[int]int)

for _, x := range a {
    count := digitCount(x)
    num2DigitCount[count]++
}

// 2 -> 1
// 1 -> 1
// 1000
// 10
// 200
// 20
// (10 * 100) + 10
// (10 * 10) + 2
// (2 * 100) + 10
// (2 * 10) + 2
// 100(10 + 2)
    for _, x := range a {
        for k, v := range num2DigitCount {
            factor := int64(1)
            for i := 0; i < k; i++ {
                factor *= 10
            }
            //fmt.Println(fmt.Sprintf("Adding %d * %d * %d", x, v, factor))
            res += int64(x) * (int64(v) * factor)
        }
        res += int64(x) * int64(len(a)) // 20 + 4
    }

return res
}

func convertBST(root *TreeNode) *TreeNode {

    stack := []*TreeNode{}
    node := root
    runningSum := 0
    
    for (len(stack) != 0 || node != nil) {
        for node != nil {
            stack = append(stack, node)
            node = node.Right
        }
        
        // pop the last item off the stack
        lastIndex := len(stack) - 1
        node = stack[lastIndex]
        stack = stack[:lastIndex]
        runningSum += node.Val
        node.Val = runningSum
        // we are at the hrightmost, go leeft once
        node = node.Left
    }
    
    
    
    
    return root
    
}

```