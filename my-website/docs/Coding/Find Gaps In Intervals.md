- Similar to merge intervals problem, but finding gaps instead. Can be done in linear time with storage tradeoff (similar to line drawing for stacked intervals).

- Data was given like [(1,2), (5,1)] where the first coord was the position, then the second number was added to and subtracted to form the interval (as in, start = pos - dist, end = pos + dist)

- Can you bitflagging (i.e. one bit per position)

- for each interval, flag from start to finish

- start from start to end, when you see a 1, toggle and push back the current interval
dont forget the last one

- can also break it up using multi-threading similar to image-processing

- can also use interval tree