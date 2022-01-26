# How to pick a good git flow

References

- The GitHub flow - 2011: http://scottchacon.com/2011/08/31/github-flow.html
- The GitLab flow - 2014: https://about.gitlab.com/blog/2014/09/29/gitlab-flow/ 
- Feature driven development: https://en.wikipedia.org/wiki/Feature-driven_development
- Microsoft git flow and branching guidance: https://docs.microsoft.com/en-us/azure/devops/repos/git/git-branching-guidance?view=azure-devops 


Picking a correct git flow is important to make sure the code that is going to produciton is really the code that was validated and tested throughout all the develompment cycle. And this git flow can vary depending on the type of project is currently being developed.

For example if this is an website, we have only one version on this website running on production so there is only one `main` line branch we support.

Another example is a desktop application that target multiple OS. Maybe we have 3 `main` versions (Linux, macOS, Windows). So that would change the flow.

Another one would be a library with multiple LTS versions. Where we support the main line and also bugfixes on LTS versions.

Also, besides the type of project, one key point as well to be aware of is the level of parallel work that will be done on this repository. Imagine 30 Pull requests being opened daily to the main branch? or dev branch?

So the type of repository and the level of parallel work are very important in order to decide which flow to follow and the links on the references could be a good guidance in order to decide which one to follow.