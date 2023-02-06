Leaders are owners. They think long term and don’t sacrifice long-term value for short-term results. They act on behalf of the entire company, beyond just their own team. They never say “that’s not my job."

## Volunteering for stuff (DEATH TO TECH DEBT)
### Situation:
- Many times, situations come up that are not well-defined nor owned by a specific team. They require volunteers to "make it happen". Examples of this were the L5 deprecation, Python Migration, and PromQL Migrations.

### Task:
- Migrate codebases from one version of Python to another. Fix unit tests and edge cases.
- Migrate from Wavefront to PromQL for reliability and speed purposes (SEVs). Metrics were being delayed and the CTO made the executive decision to fix it. The question was, whose responsibility was it? Part of it was to be done by volunteers.
- Deprecate resources that were not used anymore after an acquisition (not even remotely related to my job, team, or org, but its ok)

### Action:
- Dig deep into why the builds and tests are failing - check them out and (i.e. why is this thing using Java? oh we need to upgrade the java build version too) How is this file generated? Let's go find the SME on this or person who built it. Are there docs? No? Well let's be curious.
- How do we know resources aren't being used? What are their upstreams and dowstreams? What is the deprecation process?
- Learn some common patterns between WF and PQL (some could be automated, but some not)
- Hundreds of dashboards / alarms were migrated. There was some automation involved as well (which could be used by others)
- Look at others for patterns, read the docs about all of it
- Scan for unused resources, but requires some manual intervention (i.e. k8s reosources)
- Ruthlessly prioritize to keep the main projects moving forward along with the volunteer projects.

### Result:
- Raise awareness of team and work (helpful for XFN future)
- No more wasted resources (save $$$)
- No more reliance on wavefront, which helps in SEV situations - metrics are now more available without lag and reliable.
- Its important to upgrade libraries and use modern versions - this is reducing technical debt. The worst situation is when there is "append-only" code which nobody wants to touch because its brittle.
- Got a badge on my profile :), and migration ran smoothly
- Even being on leave for 3 months I still had more tickets completed according to JIRA for 2022
- The tradeoffs here are spending time and effort upfront for long-term benefits.
- Today there could be even more automation in migrations. We did reach the goal, but it could always be faster and less error-prone (less manual).

### Reflection:
- Make sure you know your SMEs - Network is your networth (CRINGE) - volunteering is always a learning opportunity
- Make sure you know your tracking tech (jira or whatever) (don't use google docs lol)
- Make sure both your manager and skip (in some cases) are ok with you volunteering - make sure expectations always line up.
- Automatic garbage collection is the future (especially k8s) - later on teams were established with automated processes which track these "idle resources"
- Eventually the service deprecation process will be automated as well (reason why its low prio is because it doesn't happen often)

### 5 Whys:
- What other alternatives are there to PromQL? Its industry standard, and its always better to move towardrs industry standards. This reduces onboarding time and TTR.

### Q&A:
- What would have happened if you didn't do this? There would have been wasted resources but no one would have noticed for a while. Ideally, the acquisition would include a deprecation of resources, but the reality is that sometimes things fall through the cracks, so that's where I come in, I do jobs other people don't want to do (cringe).



## Feedback Tickets
### Situation:
- something about feedback tool / automated jira requests

### Task:
- Need an organized way to collect feedback about an internal tool

### Action:
- BE:
- FE:
- working with designer for icons

### Result:
- nps / csat score
- Extracted the components into a library which can be used by other tools, all they need is a db
- hundreds of feature requests fulfilled


### Reflection:
- all about the data
- Next step would be apps or browser extensions with things like notification support, survey support, etc
- h
- h
- h

### 5 Whys:

### Q&A:



## Spelling Error On Website:
### Situation:
- I noticed a spelling error on a public facing Lyft website for safety. It had been there for years and apparently no one else cared.
  
### Task:
- Fix it.

### Action:
- I started by searching around in github repositories (using sourcegraph and github code search) trying to find the site. This came up fruitless. I next tried searching through the AWS buckets but that was difficult as there was over 50 PB of data and it was hard to find. So eventually after searching around I started contacting people. Most people weren't sure who to contact, but eventually after being persistent I found some people that were in charge of the Contentful system and could update it.

### Result:
- Lyft looks more professional. This spelling error was also highly visible because it was replicated in metadata, which led to it being displayed everytime someone shared a tweet or any kind of social media which utilized the metadata. This wasn't my responsibility at all but I took ownership because that was the right thing to do.

### Reflection:
- Its all about knowing who is in charge of what so things can be quickly fixed.

### 5 Whys:
- uwu
- 

### Q&A:
- uwu