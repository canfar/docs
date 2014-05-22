# Issues for CADC


We are investigating possibilities for a single framework for tracking development and maintenance within CADC, or at least CANFAR. The feature list is the following

* Integration: "user stories", software bugs, operations issues, features requests into one single tracking system
* Grouping: multiple issues into into one group, and across repositories for iteration planning and releases
* Tagging: tag issues by type (feature request, bug, operations, storage,...) 
* Assigning: issues can be assigned or de-assigned to any developers, common to various repositories
* Open: users can search, browse, open new issues, and comment on existing issues
* Anonymous: somehow keep a portal for anonymous users who don't like to
* Timing: set deadlines, time tracking
* Maintenance: hopefully we would use services so we don't rely on our or SSC for maintaining the tracking framework
* Filtering: avoid as much as possible the need of a human to filter the various issues at first (the helpdesk bucket model)
 

The table below summarizes the features explored for 4 different solutions.


| Solution      | Integration   | Grouping  | Tagging | Assigning | Open | Anonymous | Timing | Maintenance | Filtering |
| ------------- |:-------------:|:---------:|:-------:|:---------:|:----:|:---------:|:------:|:-----------:|:---------:|
| GitHub        | yes           | plugin    | yes     | yes       | yes  | plugin    | plugin | free service| machine   |
| BitBucket     | yes           | ???       | ???     | ???       | ???  | ???       | ???    | pay or us   | ???       |
| GitLab        | ???           | ???       | ???     | ???       | ???  | ???       | ???    | pay or us   | ???       |
| Redmine       | ???           | ???       | ???     | ???       | ???  | ???       | ???    | pay or us   | ???       |


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

Many time-tracking web-hooks or plugins to GitHub exist: [Freckle](http://letsfreckle.com) ($159/month), [Harvest](http://www.getharvest.com) ($99/month), [PivotalTracker](http://pivotaltracker.com) ($100/month), [JIRA]($150/month) are some examples. [Planbox](http://www.planbox.com) (non-profit discount). All those time-tracking are integrated with issue tracking, which forces two sets of issues. Sometimes a connector to synchronize issues exists. [Basecamp](https://basecamp.com/) ($20/month) together with maybe their communication tool Campfire might be the cheaper alternative. Full intergation framework such as [asana](http://asana.com) or [Redbooth](http://redbooth.com) are also possible, but not free. [zapier](http://zapier.com) seems to make the link between issue databases.

We can also maintain our own time-tracking on top of GitHub issues. There are opensource GitHub plugins for to 
[time track](https://github.com/StephenOTT/GitHub-Time-Tracking) together with [analytics](https://github.com/StephenOTT/GitHub-Analytics). These plugins need MongoDB and are installed as Ruby app. Tested on an OpenStack VM, they are quite clumsy and would need much tuning to get them up and working.

[Time-Tracker](https://timer.scm.io/) is a simple free app that allows to count time spent on GitHub issues.


## GitLab

## BitBucket

BitBucket integrates nicely with JIRA being from the same company. It basically would need the same time tracking as GitHub, but the alternatives in this case are pretty much all Atlassian based.

## Redmine


