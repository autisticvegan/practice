Leaders are never done learning and always seek to improve themselves. They are curious about new possibilities and act to explore them.

## Automated FE Testing

### Situation:
- Project lacked FE tests and couldn't do autodeploys.

### Task:
- Add some way of FE testing. I had the idea because of past projects that involved web scraping and automation.

### Action:
- Make the scripts that do the testing
- Basically use the Playwright (FKA Puppeteer) API and docs to figure it out.
- One reason why this wasn't the best approach was that things were always evolving. This is more about smoke tests than unit tests. Unit Test Pyramid. So storybook is the answer!
- Had to get auth tokens (needed a little non-code work)

### Result:
- Nowadays with more modern versions of React, RTL, and better versions of material this automated testing is no longer necessary. It was a nice project though.
- Can now autodeploy, saving engineer minutes every day. AUtomation is great

## Intern project

### Situation:
- People want to create new repositories but have to use metaservice (sets up repos, permissions, terraform, etc)
- To do this, they modify some files, which can be tedious and error-prone
- Sometimes it can take a long time to get the PRs approved

### Task:
- Provide a layer of abstraction using the GitHub API for modifying metaservice.
- Have the ability to message on Slack or comment “/ptal” on the PR to notify people
- Originally was going to be in AIM but then moved to Clutch

### Action:
- Added a workflow using protobufs, react, and golang
- Implemented the function createRepository along with helper functions (i.e. commenting on a PR)
- Made some tests and stuff
- dashboards, metrics for monitoring etc

### Result:
- People can now use Clutch to create new repositories
Learned a lot about React.js, protobufs and Golang
- open source is great
- Why not use backstage? Backstage is a somewhat different use case