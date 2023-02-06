Leaders are never done learning and always seek to improve themselves. They are curious about new possibilities and act to explore them.

Secret Sauce

IMPORTANT

automated FE testing

Situation:

Task:

Action:

Result:

Reflection:



## Intern project

# Situation:
- People want to create new repositories but have to use metaservice (sets up repos, permissions, terraform, etc)
- To do this, they modify some files, which can be tedious and error-prone
- Sometimes it can take a long time to get the PRs approved

# Task:
- Provide a layer of abstraction using the GitHub API for modifying metaservice.
- Have the ability to message on Slack or comment “/ptal” on the PR to notify people
- Originally was going to be in AIM but then moved to Clutch

# Action:
- Added a workflow using protobufs, react, and golang
- Implemented the function createRepository along with helper functions (i.e. commenting on a PR)
- Made some tests and stuff

# Result:
- People can now use Clutch to create new repositories
Learned a lot about React.js, protobufs and Golang

# Reflection:
- 
