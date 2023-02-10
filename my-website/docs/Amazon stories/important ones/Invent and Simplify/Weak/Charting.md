
Leaders expect and require innovation and invention from their teams and always find ways to simplify. They are externally aware, look for new ideas from everywhere, and are not limited by “not invented here." As we do new things, we accept that we may be misunderstood for long periods of time. (this is a weak category)


## Using libraries for things like Timeline Charting (weak)
### Situation:
- D needed a timeline

### Task:
- Build a view that ties together the API events coming from the BE and allows developers to map out potential relationships between them

### Action:
- Did research and figured out that the current offerings didn't really make sense for current project
- The use case existed in a space not covered by libraries, a middle ground between graphing/charting on one side and on the other event time lines / historical views. The Y-axis did not really have a use case - it also needed to be able to be merged or customized. Zooming was also useful.
- At first, tried to contribute to upstream, but they were too slow, so forked and went faster
- Encountered some weird state management bugs, but eventually fixed them with persistence
- Added tick marks to the library and other things
- state, colors, iteration with design and feedback loops
- Always focus on BE and data

### Result:
- Many people used it and were happy
- Think about the fact that the less people that use it the better - that means there's less incidents
- concept later reused in other projects

### Reflection:
- Forks are important, or at least the activity/speed of an external library
- Charting is hard (look at the graveyard)

### 5 Whys:

### Q&A: