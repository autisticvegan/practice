Minimum Total Distance Traveled

![](./maxTotalDistTraveled.jpg)
There are some robots and factories on the X-axis. You are given an integer array robot where robot[i] is the position of the ith robot. You are also given a 2D integer array factory where factory[j] = [positionj, limitj] indicates that positionj is the position of the jth factory and that the jth factory can repair at most limitj robots.

The positions of each robot are unique. The positions of each factory are also unique. Note that a robot can be in the same position as a factory initially.

All the robots are initially broken; they keep moving in one direction. The direction could be the negative or the positive direction of the X-axis. When a robot reaches a factory that did not reach its limit, the factory repairs the robot, and it stops moving.

At any moment, you can set the initial direction of moving for some robot. Your target is to minimize the total distance traveled by all the robots.

Return the minimum total distance traveled by all the robots. The test cases are generated such that all the robots can be repaired.

Note that

    All robots move at the same speed.
    If two robots move in the same direction, they will never collide.
    If two robots move in opposite directions and they meet at some point, they do not collide. They cross each other.
    If a robot passes by a factory that reached its limits, it crosses it as if it does not exist.
    If the robot moved from a position x to a position y, the distance it moved is |y - x|.



    Imagine that all factories were actually singletons (both words sound like design patterns stuff, but it's not the case), i.e., capable of repairing only one robot. The robot with the minimal coordinate will be repaired at some factory (let's say, factory A), and then this factory can no longer be used. The next robot will be repaired at some other factory (let's say, factory B). However, for the optimal solution (assuming that coordinates of robots and factories are sorted), the factory B can not come before factory A (otherwise, we would use it for the first robot). Thus, for a sequence of robots (with the increasing coordinates), there is a sequence of singleton factories with non-decreasing coordinates (in my approach, singleton factories are allowed to have same coordinates).


    Our task is to find such non-decreasing subsequence of singleton factories that minimizes the sum of distances between each robot and its assigned singleton factory. Here, DP comes into play. For, e.g. robots [9, 11, 99, 101] and singleton factories [7, 10, 14, 96, 100, 103], we should extract precisely those green distances (picture on the left) that result in the best total distance (picture on the right) for i+1 robots and j+1 factories. Thus, for each robot, we check whether each of subsequent factories (those coming after the last used one) would improve (minimize) the total sum.


    Note that for each robot we should only check m-n+1 factories (all except those colored in red), where m is the number of factories and n is the number of robots. This is due to the fact that
    ```
        for the i-th robot, we should assign at least i-th factory and
        for remaining x robots, we should have available at least x terminal (right-most) factories.
```

    Finally, for non-singleton factories (those specified in the problem) with limit L, we replicate L singleton factories at the same position, namely, [[2,1], [3,4], [7,2]] -> [2,3,3,3,3,7,7], and use the discussed approach.



```
func minimumTotalDistance(robot []int, factory [][]int) int64 {

    lenRobs := len(robot)
    lenFacs := len(factory)

    dp := make([]int64, lenRobs + 1)
    for i := 0; i < len(dp); i++ {
        dp[i] = 99999999999999
    }
    dp[0] = 0
    sort.Slice(robot, func(i, j int) bool { return robot[i] < robot[j] })
    sort.Slice(factory, func(i, j int) bool { return factory[i][0] < factory[j][0] })

    for j := 0; j < lenFacs; j++ {
        for k := 0; k < factory[j][1]; k++ {
            for i := lenRobs - 1; i >= 0; i-- {
                dp[i+1] = min(int64(abs(robot[i] - factory[j][0])) + dp[i], dp[i+1])      
            }
        }

    } 

    return dp[lenRobs]
}
```