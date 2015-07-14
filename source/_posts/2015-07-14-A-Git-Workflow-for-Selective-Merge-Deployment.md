---
title:  "A Git Workflow for Selective Merge Deployment"
date:   2015-07-14 14:38:19
categories: Git
tags: Git
author: Bigruan
---

A decent Git workflow can save your time and make your life easier when collaborating with team members. There are several well known git workflow in the wild.
[Centralized Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows), [Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow),
[Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow), [Forking Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow)

They fit for different size of project and team. *Gitflow* is widely use in the larger team and it handles a more complicated scenario. It basically has two branches, *master* is the production branch,
and *develop* is the branch which all the *feature* branches be merged to. When new features are enough for next release or it's getting to the next release date, creating a *release* branch from *develop*. From now 
on, no new features should be merged to *release* except bugfixes. A *hotfix* branch should be created from *master*, and be mergerd back to *master* and *develop*.

But for the team which has the requirements that not all the features need to go to production in the next release. It is a little difficult to handle this case because all the commits from *feature* branch are merged
into *develop*. This is a real world scenario for those team who has *QA* environment. Because all the features should be in this branch and be well tested in this environment.

Cherry-pick from develop to master may work but it's not decent enough and you need to do it carefully in order not to forget some commits. So here comes out a Variant version of gitflow which takes selective merge 
into consideration.

![gitflow_new](/images/new_git_flow.png)

- A new branch *staging* is created from *master*. This branch should never be touched until the next release. In another word, *master* and *staging* should be always the same.
- Feature branches should be created from *staging*.
- *dev/qa* branch should be initially created from *staging*.
- When feature is done, merge it to *dev/qa* for QA testing.
- For features which are going to involved in the next release, send pull request from *feature* to *staging* and the reviewer should review and merge it.
- Always create *hotfix* branch from master and merge it back when bug resolved. Also remember to merge it to *staging* and do *cherry-pick* from *dev/qa* so that the fixes are applied to both environment. If needed, send pull request from hotfix to master and staging.
- When *staging* is ready for production, merge it to *master* and give it a tag.

#### Notice

- Merging feature branches from *dev/qa* and resoving the conflicts there. DO NOT do this at feature branch.
- Remember the hotfix and apply it to both *staging* and *dev/qa*.
- Alway send pull request from *feature* to *staging*, so that the reviewers can review and merge it.
