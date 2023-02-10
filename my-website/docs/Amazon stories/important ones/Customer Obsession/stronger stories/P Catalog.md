Leaders start with the customer and work backwards. They work vigorously to earn and keep customer trust. Although leaders pay attention to competitors, they obsess over customers.  

## P Catalog (strong one)
### Situation:
Services follow a lifecycle.
REDACTED is the next generation interface for L engineers to manage their projects, enabling fast, efficient, and secure delivery of code and configuration to production. P Catalog is the foundation of REDACTED, allowing engineers to view project details in a single place, with the goal of making the service lifecycle updates fast, efficient, and secure.  It is also important to keep open source in mind, since other companies are interested such as Microsoft, Mercari, VW, and Expedia.

- Risk and Conseq if nothing happened: developers waste time and leave company, even saving minutes is valuable
- Why did I choose this story: IT has a focus on end users

### Task:
- Design
- Gather Requirements
- Architecture
- Implementation

### Action:

- building protobufs
- Building backend
- building frontend
- Iterative design - low fidelity, high fidelity, MVP, iterate (figjams, figma, code)
- Requirements - open source (quality bar), submodule, used by companies
- Achitecture has project manifests being read into topology cache, which feeds fe, fe talks to grafana, kibana, pagerduty, deploys, k8s, systems
- Stored stuff in topology cache - what were the tradeoffs? Ease of use, familiarity, making things intuitive for future engineers, keeping things as Open-sourceable as possible 
- Extending components from DASH (work smarter not harder) - Dash was meant for triaging, whereas PC is more about the service lifecycle
- DASH had similarities - ingestion, centralizing views into a SPoG, proxying, UI elements
- APIs were reused - cacheing etc
- Quicklinks - reused in DASH etc, components, images (talk about issue with webpack, using github as an image CDN because binary size, also s3 doesnt work because opensource/permissions), backend
- Differentiation between projet types - tool vs service vs library
- Configuration of manifests
- Deep links to other systems
- Deploy system enhancements
- External contributions (xfn across teams and orgs)

### Result:
- Happy customenrs (REALLY IMPORTANT) - slack messages, can talk about how this is differentiated from D as well
- nps score and csat score
- prevent SEVs and lead to faster resolution
- Positive feedback from engineers via slack about many topics - ex. during an outage they are able to more effectively debug due to things like oncall. Over 50% of engineering using it at least once a month
- The links were effective at getting users to other parts of Clutch as well (Google analytics, DORA metrics), launch point discovering
- This is about building a platform for others to build on

### Reflection:
- Platforms are great
- Similar to OpsLevel or Cortex.io (startups focused on this topic)
- User suggestions / feedback are great
- Audit log card - future improvement / audit log stuff
- Networking - added later
- Migration card - replace mode reports
- Could have some sort of tagging system / metadata system for projects
- What could be improved? Estimation, method of doing tickets, customer video interviews before design (formal questions with UX researcher)

### 5 Whys:
- Why did you use React/Typescript? - This is what was used in Clutch, it is industry standard, and convenient.
- Why did you use gRPC? - same as above
- Why topology cache? - started originally as a k8s thing, but grew into a life of its own
- Did you use a database? yes
- What was the hardest part? - customer obsession, github CDN
- Why use gRPC and not JSON? - speed, weight
- Why clutch? Familiarity
- Why open source? - Maintain higher standard of quality, and reuse in other places, also its good just like DEI

### Q&A:
- What was the scalability of this system? - it didn't matter since its less than 1 QPS. However it can easily scale to a very large number of services (think about ingestion of aggrefest). There are also built in mechanisms for when external APIs fail.
- Did this system use a database? - Yes, audit logs, topocache
