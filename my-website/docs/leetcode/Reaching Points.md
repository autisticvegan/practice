780. Reaching Points

Given four integers sx, sy, tx, and ty, return true if it is possible to convert the point (sx, sy) to the point (tx, ty) through some operations, or false otherwise.

The allowed operation on some point (x, y) is to convert it to either (x, x + y) or (x + y, y).

```
/*
why (ty-sy)%sx == 0?
since
sy will translate to ty only by (sx+sy), if they translate then (sx, sy+k*sx) = ty for some k
sy+k*sx = ty => (ty-sy) / sx = k.
Since sx,sy,tx,ty are all integer, then k has to be a integer which means, there must be a integer k that help us to reach ty. Which makes reminder to be 0
Hence
(ty-sy) % sx == 0

Basically you have a decision tree, and when doing mod, you are jumping up in a straight line this decision tree
So with a few of these jumps you can go all the way to the top
*/

func reachingPoints(sx int, sy int, tx int, ty int) bool {
    for sx < tx && sy < ty {
        if tx < ty {
            ty %= tx
        } else {
            tx %= ty
        }

    }

    xEqual := sx == tx
    yLess := sy <= ty
    yModX := (ty - sy) % sx == 0
    xMeets := xEqual && yLess && yModX

    yEqual := sy == ty
    xLess := sx <= tx
    xModY := (tx - sx) % sy == 0

    yMeets := yEqual && xLess && xModY

    return xMeets || yMeets
}

```