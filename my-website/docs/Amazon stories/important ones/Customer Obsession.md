Leaders start with the customer and work backwards. They work vigorously to earn and keep customer trust. Although leaders pay attention to competitors, they obsess over customers.  

## Project Catalog (strong one)
### Situation:
Services follow a lifecycle.
REDACTED is the next generation interface for Lyft engineers to manage their projects, enabling fast, efficient, and secure delivery of code and configuration to production. Project Catalog is the foundation of REDACTED, allowing engineers to view project details in a single place, with the goal of making the service lifecycle updates fast, efficient, and secure.  It is also important to keep open source in mind, since other companies are interested such as Microsoft, Mercari, VW, and Expedia.

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

## DASH  

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

### Q&A:
- uwu

## More Management based story (kinda weaksauce):
### Situation:
- A new deploy system was being created. Diverse perspectives were sought out to make the product better.
- The old deploy system was showing signs of age - it was built before K8s was widely adopted, and hadn't been updated in a long time. It was built on top of various products like Jenkins which had other issues. It was also bulit for smaller scale and simpler times. There have been many requests for new features, and it was time to completely overhaul the FE experience.
  
### Task:
- Gather perspectives on what users want in the new deploy system.

### Action:
- Started by started making a document for interview questions.
- Collaborate with others on this document to decide on which questions to ask. The interviews will also be recorded for others to analyze.
- Work with UI specialists on both the interview process and interviews themselves. These people were experienced in conducting useability interviews so they had valuable insights. They knew how to lead people without giving them all the answers, and how to phrase questions around what is important and defineable rather than more ambiguous ones.
- The actual interviewees were reached out to in various ways, through slack, email, and w-o-m. Some didn't respond, and some took following up, but in the end an effective cross-section of the user population was gathered. In addition to "user-population-APIs", usage logs of other tools were utilized to see who would be good to reach out to (audit logs, specific actions, etc.)

### Result:
- Note engineers, and especially infrastructure engineers, are very different customers from product engineers, or consumers.
- When the product was done, users found it to be a great experience, with over 90 NPS score.
- Note that other projects also were also improved with this process - everytime there are useability studies everyone wins.

### Reflection:
- Relationships are important - the stronger the network, the better the feedback sessions will be, because people will prioritize your product's research over potential other tasks, and also will have higher trust which will lead to more comfortable feedback.
- In the future, there could be better bifurcation between roles and interests to make sure we are getting the full picture of users. Sometimes its hard to divide - is this engineer a service engineer? ops? reliability? automation? test? product? What does product even mean in this context?
- It would be interesting to look at other useability interviews throughout the history of the company and other products.

### 5 Whys:
- uwu

### Q&A:
- uwu
