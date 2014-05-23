# Issues and repositories for CADC


We are investigating possibilities for a single framework for tracking development, software maintenance and project management within CADC, or at least CANFAR. We are focusing on 4 popular open frameworks, which all integrate code repository, issue tracking and some kind of project management. We focus on the features which are not always available for all:

* **Grouping**: multiple issues into into one group, and across repositories for iteration planning and releases
* **Anonymous**: somehow keep a portal for anonymous users who don't like to
* **Timing**: set deadlines, set issue or story time tracking, generate reports
* **Maintenance**: how much maintenance we would have to do
* **Review**: if code review is possible
* **CI**: continuous integration

The table below summarizes the features explored for 4 different solutions.


| Solution      | Grouping  | Anonymous | Timing  | Maintenance | Code Review |    CI   |
| ------------- |:---------:|:---------:|:-------:|:-----------:|:-----------:|:-------:|
| GitHub        | plugin    | plugin    | plugins | none        | built-in    | plugins |
| BitBucket     | ???       | built-in  | plugins | none        | built-in    | plugins |
| GitLab        | ???       | ???       |  ???    | yes         | built-in    | plugins |
| Redmine       | ???       | ???       | plugins | yes or pay  | plugins     |  ???    |


## GitHub

#### Grouping:

Grouping issues is done through milestones.

* a milestone within one repository can be defined, and containing multiple issues 
* a milestone could be defined either as a user story or a list of tasks within a story
* no milestones across repositories
* Webhooks:  
  * [Waffle](http://waffle.io) is a an external service using GitHub issue API that presents a typical Kanban dashboard. Milestones with the same name across different repositories can be defined and the service will recognize it.
  * [HuBoard](http://huboard.com) is another similar service for Kanban board. It looks too minimal, but may be some plugins are possible.

#### Anonymous

A user has to be registered with GitHub to file an issue to CANFAR. 

The external service [GitReports](http://gitreports.com/) can be used to cover the full Github CANFAR organization and allow anonymous user reports. It is free, but we can also maintain the GitReports application ourselves, may be we can add LDAP signing to it instead of anonymous reports.


#### Timing

GitHub milestones can be defined with a deadline, but no time tracking is done. Comment on time tracking from GitHub:

"One thing to keep in mind is such time-tracking tools don't accurately capture all the time spent developing software. We generally want to encourage developers to take the time for important software development tasks that don't involve coding directly such as filing detailed issues, creating pull requests, and conducting testing and design work that live outside of GitHub. Most time-tracking tools don't achieve this alone."

Many time-tracking web-hooks or plugins to GitHub exist: [Freckle](http://letsfreckle.com) ($159/month), [Harvest](http://www.getharvest.com) ($99/month), [PivotalTracker](http://pivotaltracker.com) ($100/month), [JIRA](https://www.atlassian.com/software/jira) ($150/month), or [Planbox](http://www.planbox.com) ($129/month, may be non-profit discount) are some examples. All those time-tracking systems are integrated with some issue tracking, which sometimes means two sets of issues: GitHub and the time-tracking system issue. Sometimes a connector to synchronize issues exists. [zapier](http://zapier.com) seems to make the link between issue databases. [Basecamp](https://basecamp.com/) ($20/month) together with maybe their communication tool [Campfire](https://campfirenow.com/) ($29/month) might be the popular cheaper alternative. Full intergation project management framework such as [Asana](http://asana.com) is also possible, it has 3 time tracking plugins possible, and integrate with GitHub. Might be overkill for our projects. or [Redbooth](http://redbooth.com) is another (non free) task management full featured app. All prices cited have been chosen given the size of our team as 20 people.

We can also maintain our own time-tracking on top of GitHub issues. There are opensource GitHub plugins for to 
[time track](https://github.com/StephenOTT/GitHub-Time-Tracking) together with [analytics](https://github.com/StephenOTT/GitHub-Analytics). These plugins need MongoDB and are installed as Ruby app. Tested on an OpenStack VM, they are quite clumsy and would need much tuning to get them up and working.

[Time-Tracker](https://timer.scm.io/) is a simple free app that allows to count time spent on GitHub issues.


## GitLab

Seems very popular, emulates GitHub features, locally. Sites are down.

## BitBucket

BitBucket integrates nicely with JIRA being from the same company. It basically would need the same time tracking as GitHub, but the alternatives in this case are pretty much all Atlassian based.

## Redmine


