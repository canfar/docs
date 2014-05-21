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
* Plugins (as external services):  
  * http://waffle.io presents a typical agile dashboard. milestones with the same name across different repositories can be defined and the service will recognize it
  

#### Anonymous

A user has to be registered to file an issue.

The http://gitreports.com/ can be applied for our site, or we can also maintain it for anonymous user reports.


#### Timing

milestones can be defined with a deadline, but no time tracking is done. Comment on time tracking from GitHub:

"One thing to keep in mind is such time-tracking tools don't accurately capture all the time spent developing software. We generally want to encourage developers to take the time for important software development tasks that don't involve coding directly such as filing detailed issues, creating pull requests, and conducting testing and design work that live outside of GitHub. Most time-tracking tools don't achieve this alone."

Here is a list of possible services to be used as time trackers:

1. http://letsfreckle.com/ has a pre-built web-hook for time tracking. It can be enabled per repository. TO BE TESTED
2. https://github.com/klokantech/github-time-tracking TO BE TESTED
3. https://github.com/StephenOTT/GitHub-Time-Tracking TO BE TESTED
 


## GitLab

## BitBucket

## Redmine


