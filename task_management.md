Integrated Task management tools
============================

This documents tries to list requirements for task management systems, and the tools some of us have tried. It also has another section concerning communication/chat tools and integration with the task management.

All tools reviewed below should satisfy the requirements called **Mandatory**. 
There are some **Optional** requirements. The tools satisfying these optional requirements are listed in the table.  

Task management tools requirements
---------------------------------------------
The idea is to not only solve the unpleasant RT  experience, but also to integrate user issues, project management, communications and possibly other tools we are using or should be using. Hopefully that would make both the user and our own experience more pleasant and efficient.

The requirements are vague enough to let us have the possibility to switch not just to another RT system, but to switch to a different procedure than an RT-like process.

#### Mandatory
The tool:

 - must have user issue management features: reporting, tracking, assigning, searching (for CADC users)
 - provides project management (agile style was assumed mandatory) integrated with issue tracking
 - can manage task grouping:  project, epics, user story, task, issue...
 - can do reports and/or task analytics 
 - can manage task dependencies
 - tracks task time (or "point")
 - has an interface we can access everywhere (meaning a web interface to a server hosted on a public IP VM)
 - integrates with git, i.e. in the form of a web repository viewer
 - integrates with a chat tool: the table will list in the column **Chat** the integration with chat tools, and if it integrates with all, a subjective indication to which one it integrates best with

#### Optional

The tool can support:
 - **Email**: issue creation should be possible via email (such as: submit issues to support@blah.org)
 - **LDAP**:  user authentication could be done with LDAP
 - **Mobile**: both Android & iOS apps are supported

Notes:

 - **Cost**: reported costs are in USD / 30 internal users / year. Open Source Software (OSS) means the cost is our labour, or in all those cases, a paid service tier can maintain it for us.  
 - **Examples** : see links for some projects using those tools
 
 
| Solution      | Cost | Chat| Email | LDAP | Mobile | Examples | Comments  |
| ------------- |-----:|:---:|:-----:|:----:|:------:|----------|:----------|    
| [JIRA](https://www.atlassian.com/software/jira) |2,040| all, HipChat | [desk](https://www.atlassian.com/software/jira/service-desk) |yes| yes|[demo](https://jira.atlassian.com/browse/DEMO/),[cern](https://its.cern.ch/jira/secure/Dashboard.jspa)|need JIRA Agile + JIRA Service Desk + Confluence. [free for OSS](https://www.atlassian.com/software/views/open-source-license-request)|
| [Yodiz](http://www.yodiz.com/)| 1,800 |[slack?](http://yodiz.uservoice.com/forums/147983-general/suggestions/6367135-integrate-with-slack) | yes | no | yes |[videos](https://www.youtube.com/results?search_query=yodiz)|[free for academic](http://www.yodiz.com/free-agile-software.html)|
| [Rally](https://www.rallydev.com/)  |[10,000](https://www.rallydev.com/platform-products/rally-editions)| Flowdock | ?? | yes | yes | |great for intranet, extranet not clear|
| [YouTrack](https://youtrack.jetbrains.com/) |1,500 | XMPP | yes | yes | yes |[video](https://www.youtube.com/watch?v=d7oSxVVzb2A)|[free for OSS](https://www.jetbrains.com/youtrack/buy/open_source_incloud.jsp)
| [PivotalTracker](http://www.pivotaltracker.com/)| 3,000 | all, Flowdock| yes | no | yes |[projects](http://www.pivotaltracker.com/community/public-projects)|[free for public or academic](https://www.pivotaltracker.com/faq#istrackerreallyfreeforpublicprojectsindividualusenonprofitsandeducators)|
| [GitHub](https://github.com/features)| 300 | all, Gitter | [yes?](https://gitreports.com/) | [enterprise](https://help.github.com/enterprise/2.1/admin/guides/user-management/using-ldap/) | yes ||  $300/y for 10 private repos, free for OSS, [project management setup](https://www.lullabot.com/blog/article/managing-projects-github) |
| [GitLab](https://gitlab.com/features)| OSS | slack, Flowdock, gitter | no | yes| yes | Cybera VM (ask seb)| agile project management might need extra software |
| [Taiga](https://taiga.io/)   | OSS | slack | yes | yes | no |Cybera VM (ask seb)|[time tracking p.o.v.](https://taiga.io/support/why-is-there-no-time-tracking/), very new|
| [Tuleap](https://www.tuleap.org/) | OSS |XMPP| yes | yes |no| [demo](https://demo-tuleap.enalean.com/account/login.php?return_to=%2Fmy%2F) | demo url unaccessible at HIA network. one stop solution for all CADC|
| [OpenProject](https://www.openproject.org/) | OSS|via bot|yes|yes|redmine?|[community](https://community.openproject.org/projects/openproject/)|chat integration seems with a chat bot only|
| [Redmine](http://www.redmine.org/)| OSS |HipChat, Flowdock, XMPP |yes|yes|yes| Cybera VM (ask seb)|most complete solution. painful to get friendly (but possible)|


Other useful links:

 - [Project Management comparison tool](http://project-management.zone/) : not always up to date
 - [Google Trend JIRA vs. Redmine](http://www.google.ca/trends/explore#q=%2Fm%2F0d5lm5%2C%20%2Fm%2F0464wfc&cmpt=q&tz=), add your tool to see whether it is popular in the google sense
 - [stackshare.io](http://stackshare.io) : look for one of the tool
 - Other tools which we have tried: [asana](http://www.asana.com), [assembla](http://www.assembla.com),  [GEMINI](http://www.countersoft.com), [Phabricator](http://phabricator.org)

Communication tools requirements
------------------------------------------

####Mandatory:
The tool must:

 - supports multi users (doh)
 - supports multi chat rooms (also called channels, or flows)
 - supports Linux and OSX access, outside from CADC as well
 - allow non-public chat rooms
 - bi-directional integration with one of the task management system above
 - integration with a deployment platform

####Optional:
The tool can integrate with:

- **Email** to the chat clients
- a calendar (**Cal**)
- **git** activity 
- a monitoring platform (**Mon**)
- continuous integration tests (**CI**)

The tool:

- can be accessed from standard chat clients via XMPP or IRC **Protocols**
- has native **Desktop** clients, standard means an all-protocols chat client such as adium (OSX), pidgin (Linux), etc...
- has native **Mobile** clients, both Android and iOS


| Solution      | Cost | Email | Cal | git | Mon | CI | Desktop | Mobile | Protocols | Comments |
| ------------- |-----:|:-----:|:---:|:---:|:---:|:--:|:-------:|--------|-----------|:----------|
| [Flowdock](https://www.flowdock.com/) | 1,080 | yes | yes | yes | yes | yes | OSX| all | IRC | splitted views, threads |
| [Slack](https://slack.com/) |2,400| yes| yes | yes | yes | yes | OSX | all | IRC, XMPP| |
| [HipChat](https://www.hipchat.com/)| 720| no | no | yes | yes | yes | all | all |XMPP| allow guest users|
| [Gitter](https://gitter.im/) |720| no | no | yes | yes | yes | all | all | IRC | splitted views|
| [Sans](http://www.sansbullshitsans.com/)| free| yes | yes | yes | yes| yes | all | all | all | revolutionary|
| [OpenFire](http://www.igniterealtime.org/projects/openfire/) | OSS| yes | yes | yes | yes | yes |standard|standard|XMPP| some integrations need work |


Other useful links:

 - Other tools which we have tried: [glip](https://glip.com), [eXo](http://www.exoplatform.com)(OSS)
 - Links about doing everything from chat (so-called ChatOps): [flowdock blog post](http://blog.flowdock.com/2014/11/11/chatops-devops-with-hubot/), [ChatOps at GitHub](https://www.youtube.com/watch?v=NST3u-GjjFw)