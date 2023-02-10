Leaders focus on the key inputs for their business and deliver them with the right quality and in a timely fashion. Despite setbacks, they rise to the occasion and never settle.

## K8s Dash
### Situation:
- engineers needed a better interface than kubectl

### Task:
- build it

### Action:
- FE, BE, open-source, protobufs, docs, links everywhere, announcment comms, k8s apis, figure out facets,
- feedbacks, metrics
- could take actions from it - required deeplinks
- sorting, data layouts, split between pods and facets
- required some changes from normal "workflow"
- reminder that auth and stuff comes out of the box

### Result:
- Quickly delivered within a month of starting
- talk about migration from l-kube
- added metrics to l-kube to track this, and made sure to redirect when possible
- autocomplete was tricky but it was do-able for the main use cases without performance issues
- people liked it, hundreds of users
- components and lessons reused elsewhere (i.e. autocomplete)

### Reflection:
- 

### 5 Whys:

- Why not something like Istio, LinkerD, or EKS? - At the time, it was an old version of K8s. It is now being migrated to EKS where tools like this will be less necessary. EKS in the early days lacked certain features around networking that were critical for the biz. 

### Q&A:
