Leaders are owners. They think long term and don’t sacrifice long-term value for short-term results. They act on behalf of the entire company, beyond just their own team. They never say “that’s not my job."

## Feedback Tickets
### Situation:
- A lot of the feedback and feature requests were coming in through various formats - slack, email, dm's, jira ticket bug reports, etc. There needed to be a way to organize this better and have it a better experience than forcing users to open new jira tickets.

### Task:
- Need an organized way to collect feedback about an internal tool

### Action:
- BE - saving to db, where mode reports can be made, jira integration, validation, protobufs for things like metadata and enums
- FE - reusable components, input box, make sure its styled correctly, icons get bigger (could animate but decided against it)
- working with designer for icons (emojis svg from png)
- Extracted the components into a library which can be used by other tools, all they need is a db

### Result:
- nps / csat score used in OKRs (> 80)
- Components reused in other areas
- hundreds of feature requests fulfilled ~100 (highest number of tickets completed)

### Reflection:
- Why not use qualtrics or something similar? Cost, complexity, sometimes building for scratch can be a better fit for your exact use-case rather than a solution which fits many use-cases.
- all about the data
- Next step would be apps or browser extensions (think about code injection) with things like notification support, survey support, etc
- Tricky to get the UX right - don't want to be intrusive, but do want to gather data i.e. popups are painful

### 5 Whys:

### Q&A:

