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
| BitBucket     | ???           | ???       | ???     | ???       | ???  | ???       | ???    | pay or us   | ???       |
| GitLab        | ???           | ???       | ???     | ???       | ???  | ???       | ???    | pay or us   | ???       |
| Redmine       | ???           | ???       | ???     | ???       | ???  | ???       | ???    | pay or us   | ???       |


## GitHub

#### Grouping:

Grouping issues is done through milestones.

* a milestone within one repository can be defined, and containing multiple issues 
* a milestone could be defined either as a user story or a list of tasks within a story
* no milestones across repositories
* Webhooks:  
  * http://waffle.io is a an external service using GitHub issue API that presents a typical Kanban dashboard. Milestones with the same name across different repositories can be defined and the service will recognize it.
  * http://huboard.com is another similar service for Kanban board. It looks too minimal, but may be some plugins are possible.

#### Anonymous

A user has to be registered with GitHub to file an issue to CANFAR. 

The external service http://gitreports.com/ can be used to cover the full Github CANFAR organization and allow anonymous user reports. Or we can also maintain the gitreports application ourselves. Another possibility is to integrate issue reporting with CANFAR 


#### Timing

GitHub milestones can be defined with a deadline, but no time tracking is done. Comment on time tracking from GitHub:

"One thing to keep in mind is such time-tracking tools don't accurately capture all the time spent developing software. We generally want to encourage developers to take the time for important software development tasks that don't involve coding directly such as filing detailed issues, creating pull requests, and conducting testing and design work that live outside of GitHub. Most time-tracking tools don't achieve this alone."

Here is a list of possible services to be used for time trackers on top of GitHub platform:

1. http://letsfreckle.com/ has a pre-built web-hook for time tracking. It can be enabled per repository. $159/month
2. http://www.getharvest.com/ another webhook. $99/month
3. https://github.com/StephenOTT/GitHub-Time-Tracking needs local maintainship (MongoDB ruby app), goes together well with    https://github.com/StephenOTT/GitHub-Analytics
4. http://pivotaltracker.com/ full service with GitHub webhook, $100/month


## GitLab

## BitBucket

## Redmine


