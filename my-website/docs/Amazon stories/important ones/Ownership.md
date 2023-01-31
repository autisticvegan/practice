Leaders are owners. They think long term and don’t sacrifice long-term value for short-term results. They act on behalf of the entire company, beyond just their own team. They never say “that’s not my job."

IMPORTANT

## Volunteering for stuff
### Situation:
- Many times, situations come up that are not well-defined nor owned by a specific team. They require volunteers to "make it happen". Examples of this were the L5 deprecation, Python Migration, and PromQL Migrations.

### Task:
- Migrate codebases from one version of Python to another. Fix unit tests and edge cases.
- Migrate from Wavefront to PromQL
- Deprecate resources that were not used anymore

### Action:
- Dig deep into why the builds and tests are failing - check them out and (i.e. why is this thing using Java? oh we need to upgrade the java build version too)
- Learn some common patterns between WF and PQL (some could be automated, but some not)
- Look at others for patterns, read the docs about all of it
- Scan for unused resources, but requires some manual intervention (i.e. k8s reosources)

### Result:
- Raise awareness of team and work (helpful for XFN future)
- No more wasted resources
- No more reliance on wavefront, which helps in SEV situations
- Got a badge on my profile :), and migration ran smoothly

### Reflection:
- Make sure you know your SMEs
- Make sure you know your tracking tech (jira or whatever)
- Automatic garbage collection is the future (especially k8s)

### 5 Whys:

### Q&A:

## Feedback Tickets
### Situation:
- something about feedback tool / automated jira requests

### Task:


### Action:


### Result:
nps / csat score

### Reflection:
all about the data

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