Thinking small is a self-fulfilling prophecy. Leaders create and communicate a bold direction that inspires results. They think differently and look around corners for ways to serve customers.

# DASH  

### Situation:
- Service Engineers often have a lot of cognitive load and need to merge information quickly when dealing with incidents and monitoring. There are many diverse systems that have to look at - Pagerduty, Grafana, Kibana, Slack, Github, deploy systems, etc. 

### Task:
- Build a system that solves these problems. Focus on service engineer persona. What do they care about?

### Action:
- Design
- Spec Writing
- //think about timeline view
- Timeline view - 

### Result:
- "Makes me want to own more services" - an engineer

### Reflection:
- What could be improved? Reaching out to maintainers of OS libraries (to uncover issues earlier)
- Estimation (Milestone doc quickly went out of date)
- User research / TPM / EM resources can be useful

### 5 Whys:
- uwu
- 

### Q&A:
- uwu


# Project Catalog  

### Situation:
- Engineers need a way to manage their projects, enabling delivery of code and config to production. Project Catalog allows engineers to view project details in a single place, with the goal of making the service lifecycle updates fast, efficient, and secure. It is also important to keep open source in mind, since other companies are interested such as Microsoft, Mercari, VW, and Expedia.

NO MORE YAML

### Task:
- Build an open source system in Clutch that solves these problems.

### Action:
- Iterative design - low fidelity to high fidelity, MVP, iterate, designers
- Use a submodule in Clutch to keep things open source - open source is important and keeps quality bar higher - also opensourced certain components (abstraction vs MVP)
- Come up with architecture
- building protobufs
- Building backend
- building frontend
- modifying the topology cache with certain funcs
- Liasoned and worked with other teams such as Networking (Envoy), Observability (APIs), and Deploys (APIs)

### Result:
- Positive feedback from engineers via slack about many topics - ex. during an outage they are able to more effectively debug due to things like oncall. Over 50% of engineering using it at least once a month
- The links were effective at getting users to other parts of Clutch as well
- This is about building a platform for others to build on

### Reflection:
- Could add Audit Log stuff
- User suggestions (user feedback is important!)
- Migration progress tracking
- What could be improved? Estimation, method of doing tickets, customer video interviews before design (formal questions with UX researcher)

### 5 Whys:
- Why use gRPC and not JSON? - speed, weight
- Why clutch? Familiarity
- Why open source? - Maintain higher standard of quality, and reuse in other places, also its good just like DEI
- 

### Q&A:
- What was the scalability of this system? - it didn't matter since its less than 1 QPS. However it can easily scale to a very large number of services (think about ingestion of aggrefest). There are also built in mechanisms for when external APIs fail.
- Did this system use a database? - Yes, audit logs, topocache
- 