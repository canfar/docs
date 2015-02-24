Integrated Task management tools
============================

This documents tries to list requirements for task management systems, and the tools some of us have tried. It also has another section concerning communication/chat tools and integration with the task management.

All tools reviewed below should satisfy the requirements called **Mandatory**. 
There are some **Optional** requirements. The tools satisfying these optional requirements are listed in the table.  

Task management tools requirements
---------------------------------------------
The idea is to not only solve the RT unpleasant experience, but also to integrate user issues, project management, communications and possibly other tools we are using or should be using. Hopefully that would make both the user and our own experience more pleasant and efficient.

#### Mandatory
 - user issue management features: reporting, tracking, assigning, searching (for CADC users)
 - integrates with project management (agile style was assumed mandatory)
 - manage task grouping:  project, epics, user story, task, issue...
 - can do reports and/or task analytics 
 - can manage task dependencies
 - tracks task time (or "point")
 - has an interface we can access everywhere (meaning a web interface to a server hosted on a public IP VM)
 - integrates with git, i.e. in the form of a web repository viewer
 - integrates with a chat tool: the table will list in the column **Chat** the integration with chat tools, and if it integrates with all, a subjective indication to which one it integrates best with

#### Optional
 - **Email** means issue creation should be possible via email (such as: submit issues to support@blah.org)
 - **LDAP** mean whether user authentication could be done with LDAP
 - **Mobile** apps (both Android & iOS)

Notes:

 - **Cost**: reported costs are in USD / 30 internal users / year. Open Source Software (OSS) means the cost is our labour, or in all those cases, a paid service tier can maintain it for us.  
 - **Examples** : see links for some projects using those tools
 
 
| Solution      | Cost | Chat| Email | LDAP | Mobile | Examples | Comments  |
| ------------- |-----:|:---:|:-----:|:----:|:------:|----------|:----------|    
| [JIRA](https://www.atlassian.com/software/jira) |2,040| all, HipChat | [desk](https://www.atlassian.com/software/jira/service-desk) |yes| yes|[demo](https://jira.atlassian.com/browse/DEMO/),[cern](https://its.cern.ch/jira/secure/Dashboard.jspa)|need JIRA Agile + JIRA Service Desk + Confluence. [free for OSS](https://www.atlassian.com/software/views/open-source-license-request)|
| [Yodiz](http://www.yodiz.com/)| 1,800 |[slack?](http://yodiz.uservoice.com/forums/147983-general/suggestions/6367135-integrate-with-slack) | yes | no | yes |[videos](https://www.youtube.com/results?search_query=yodiz)|[free for academic](http://www.yodiz.com/free-agile-software.html)|
| [Rally](https://www.rallydev.com/)  |[10,000](https://www.rallydev.com/platform-products/rally-editions)| Flowdock |?? |yes|yes||great for intranet, extranet not clear|
| [YouTrack](https://youtrack.jetbrains.com/) |1,500 | XMPP | yes | yes| yes |[video](https://www.youtube.com/watch?v=d7oSxVVzb2A)|[free for OSS](https://www.jetbrains.com/youtrack/buy/open_source_incloud.jsp)
| [PivotalTracker](http://www.pivotaltracker.com/)| 3,000 | all, Flowdock| yes | no | yes |[projects](http://www.pivotaltracker.com/community/public-projects)|[free for public or academic](https://www.pivotaltracker.com/faq#istrackerreallyfreeforpublicprojectsindividualusenonprofitsandeducators)|
| [GitHub](https://github.com/features)| 300 | all, Gitter | [yes?](https://gitreports.com/) | [enterprise](https://help.github.com/enterprise/2.1/admin/guides/user-management/using-ldap/) | yes ||  $300/y for 10 private repos, free for OSS |
| [GitLab](https://gitlab.com/features)| OSS | slack,Flowdock,gitter | no | yes| yes | Cybera VM (ask seb)|  |
| [Taiga](https://taiga.io/)   | OSS | slack | yes | yes | no |Cybera VM (ask seb)|[time tracking p.o.v.](https://taiga.io/support/why-is-there-no-time-tracking/), very new|
| [Tuleap](https://www.tuleap.org/) | OSS |XMPP| yes | yes |no| [demo](https://demo-tuleap.enalean.com/account/login.php?return_to=%2Fmy%2F) | demo url unaccessible at HIA network. one stop solution for all CADC|
| [OpenProject](https://www.openproject.org/) | OSS|via bot|yes|yes|redmine?|[community](https://community.openproject.org/projects/openproject/)|chat integration seems with a chat bot only|
| [Redmine](http://www.redmine.org/)| OSS |HipChat, Flowdock, XMPP |yes|yes|yes| Cybera VM (ask seb)|most complete solution. painful to get friendly (but possible)|


Other useful links:

 - [Project Management comparison tool](project-management.zone) : not always up to date
 - [Google Trend JIRA vs. Redmine](http://www.google.ca/trends/explore#q=%2Fm%2F0d5lm5%2C%20%2Fm%2F0464wfc&cmpt=q&tz=), add your tool to see whether it is popular in the google sense
 - [stackshare.io](http://stackshare.io) : look for one of the tool
 - Other tools which we have tried: [asana](http://www.asana.com), [assembla](http://www.assembla.com),  [GEMINI](http://www.countersoft.com), [Phabricator](http://phabricator.org)

Communication tools requirements (IN PROGRESS)
------------------------------------------

####Mandatory:
 - multi users
 - multi chat rooms (also called channels, or flows)
 - Linux, OSX access, outside from CADC as well
 - allow non-public chat rooms
 - bi-directional integration with one of the task management system above
 - integration with a deployment platform

####Optional:

- integration with **Email** to the chat clients
- integration with a calendar (**Cal**)
- integration with **git** activity 
- integration with a monitoring platform (**Mon**)
- integration with continuous integration tests (**CI**)
- integration with code review (**CR**)
- Can be accessed from general chat clients via XMPP or IRC **Protocols**
- Native **Destop** clients, generic means an all-chat kind of client (adium, pidgin,...)
- Native **Mobile** clients


| Solution      | Cost | Email | Cal | git | Mon | CI | CR  | Desktop | Mobile | Protocols | Comments |
| ------------- |-----:|:-----:|:---:|:---:|:---:|:--:|:---:|---------|--------|----------|:-----|
| [Flowdock](https://www.flowdock.com/) | 1,080 | yes | yes | yes | yes | yes | yes | OSX| all | IRC | splitted views, threads |
| [Slack](https://slack.com/) |2,400| yes| yes | yes | yes | yes | yes | OSX | all | IRC, XMPP
| [HipChat](https://www.hipchat.com/)| 720|||||||all| all |XMPP| allow guest users|
| [Gitter](https://gitter.im/) |720|||||||all|all|IRC| splitted views|
| [OpenFire](http://www.igniterealtime.org/projects/openfire/) | OSS|||||||generic|generic|XMPP||


Other useful links:

 - Other tools which we have tried: [glip](https://glip.com), [eXo](http://www.exoplatform.com)(OSS)
 - Links about doing everything from chat (so-called ChatOps): [flowdock blog post](http://blog.flowdock.com/2014/11/11/chatops-devops-with-hubot/), [ChatOps at GitHub (40mn video)](https://www.youtube.com/watch?v=NST3u-GjjFw)