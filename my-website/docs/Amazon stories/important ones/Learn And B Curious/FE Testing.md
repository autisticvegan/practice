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
