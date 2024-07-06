## Jira-CDEvents Integration

### Design-Overview:
Jira emits variuos type of events like Issue related, Project related, User related, Configuration and Software related.
[Jira webhooks](https://developer.atlassian.com/server/jira/platform/webhooks/) can be configured to notify external applications when certain events occur in Jira.

CDEvents can be integrated with Jira using CDEvents's [webhook-adapter](https://github.com/cdevents/webhook-adapter) which exposes an interface to be implemented as plugin.


### Jira-translator-CDEvents:

`jira-translator-cdevents` plugin will be implemented to translate [Jira events](https://developer.atlassian.com/platform/forge/events-reference/jira/) into CDEvents and served using Hashicorp's [go-plugin](https://github.com/hashicorp/go-plugin/).

The plugin details needs to be updated in webhook-adapter's [translator-plugins.yaml](https://github.com/cdevents/webhook-adapter/blob/main/translator-plugins.yaml) to serve as a translator endpoint, which is configured as Jira Webhook URL.

Issue related Jira events can be mapped to CDEvent's [Ticket Events](https://cdevents.dev/docs/tickets/), The below is the list of CDEvents Ticket Events will be mapped with corresponding Jira event types.



| CDEvent Type  | Jira Event Type  | Comments / Jira Event Format   |
| :------------ |:-------------------|:----------------------------------|
| dev.cdevents.ticket.created| jira:issue_created |
<details>
<summary>Event JSON</summary>

```
{
  "timestamp": 1716991458232,
  "webhookEvent": "jira:issue_created",
  "issue_event_type_name": "issue_created",
  "user": {
    "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
    "name": "rjalander",
    "key": "JIRAUSER10000",
    "emailAddress": "jalander.ramagiri@est.tech",
    "avatarUrls": {
      "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
      "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
      "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
      "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
    },
    "displayName": "jalander.ramagiri@est.tech",
    "active": true,
    "timeZone": "Europe/Dublin"
  },
  "issue": {
    "id": "10023",
    "self": "http://localhost:9090/rest/api/2/issue/10023",
    "key": "ES-24",
    "fields": {
      "issuetype": {
        "self": "http://localhost:9090/rest/api/2/issuetype/10002",
        "id": "10002",
        "description": "Created by Jira Software - do not edit or delete. Issue type for a user story.",
        "iconUrl": "http://localhost:9090/images/icons/issuetypes/story.svg",
        "name": "Story",
        "subtask": false
      },
      "timespent": null,
      "project": {
        "self": "http://localhost:9090/rest/api/2/project/10000",
        "id": "10000",
        "key": "ES",
        "name": "EST-SeaTel",
        "projectTypeKey": "software",
        "avatarUrls": {
          "48x48": "http://localhost:9090/secure/projectavatar?avatarId=10324",
          "24x24": "http://localhost:9090/secure/projectavatar?size=small&avatarId=10324",
          "16x16": "http://localhost:9090/secure/projectavatar?size=xsmall&avatarId=10324",
          "32x32": "http://localhost:9090/secure/projectavatar?size=medium&avatarId=10324"
        }
      },
      "fixVersions": [],
      "customfield_10110": "0i00053:",
      "customfield_10111": null,
      "aggregatetimespent": null,
      "resolution": null,
      "customfield_10107": null,
      "customfield_10108": null,
      "customfield_10109": null,
      "resolutiondate": null,
      "workratio": -1,
      "lastViewed": null,
      "watches": {
        "self": "http://localhost:9090/rest/api/2/issue/ES-24/watchers",
        "watchCount": 0,
        "isWatching": false
      },
      "created": "2024-05-29T15:04:18.022+0100",
      "priority": {
        "self": "http://localhost:9090/rest/api/2/priority/3",
        "iconUrl": "http://localhost:9090/images/icons/priorities/medium.svg",
        "name": "Medium",
        "id": "3"
      },
      "customfield_10100": null,
      "customfield_10101": null,
      "customfield_10102": null,
      "labels": [],
      "customfield_10103": null,
      "timeestimate": null,
      "aggregatetimeoriginalestimate": null,
      "versions": [],
      "issuelinks": [],
      "assignee": {
        "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
        "name": "rjalander",
        "key": "JIRAUSER10000",
        "emailAddress": "jalander.ramagiri@est.tech",
        "avatarUrls": {
          "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
          "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
          "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
          "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
        },
        "displayName": "jalander.ramagiri@est.tech",
        "active": true,
        "timeZone": "Europe/Dublin"
      },
      "updated": "2024-05-29T15:04:18.022+0100",
      "status": {
        "self": "http://localhost:9090/rest/api/2/status/10000",
        "description": "",
        "iconUrl": "http://localhost:9090/",
        "name": "To Do",
        "id": "10000",
        "statusCategory": {
          "self": "http://localhost:9090/rest/api/2/statuscategory/2",
          "id": 2,
          "key": "new",
          "colorName": "default",
          "name": "To Do"
        }
      },
      "components": [],
      "timeoriginalestimate": null,
      "description": "CDEvents integration with Jira",
      "timetracking": {},
      "archiveddate": null,
      "attachment": [],
      "aggregatetimeestimate": null,
      "summary": "CDEvents integration with Jira",
      "creator": {
        "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
        "name": "rjalander",
        "key": "JIRAUSER10000",
        "emailAddress": "jalander.ramagiri@est.tech",
        "avatarUrls": {
          "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
          "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
          "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
          "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
        },
        "displayName": "jalander.ramagiri@est.tech",
        "active": true,
        "timeZone": "Europe/Dublin"
      },
      "subtasks": [],
      "reporter": {
        "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
        "name": "rjalander",
        "key": "JIRAUSER10000",
        "emailAddress": "jalander.ramagiri@est.tech",
        "avatarUrls": {
          "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
          "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
          "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
          "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
        },
        "displayName": "jalander.ramagiri@est.tech",
        "active": true,
        "timeZone": "Europe/Dublin"
      },
      "customfield_10000": "{summaryBean=com.atlassian.jira.plugin.devstatus.rest.SummaryBean@6f5ce47b[summary={pullrequest=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@2658d383[byInstanceType={},overall=PullRequestOverallBean{stateCount=0, state=OPEN, details=PullRequestOverallDetails{openCount=0, mergedCount=0, declinedCount=0}}], build=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@5d1d8c4f[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.BuildOverallBean@3db998a4[failedBuildCount=0,successfulBuildCount=0,unknownBuildCount=0,count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], review=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@14ec6fe6[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.ReviewsOverallBean@fb11e8b[dueDate=<null>,overDue=false,state=<null>,stateCount=0,count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], deployment-environment=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@3eff84c6[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.DeploymentOverallBean@4ff25705[showProjects=false,successfulCount=0,topEnvironments=[],count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], repository=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@38968242[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.CommitOverallBean@3fd4869d[count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], branch=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@7d4fec15[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.BranchOverallBean@2058d6c6[count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]]},configErrors=[],errors=[]], devSummaryJson={\"cachedValue\":{\"errors\":[],\"configErrors\":[],\"summary\":{\"pullrequest\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"stateCount\":0,\"state\":\"OPEN\",\"details\":{\"openCount\":0,\"mergedCount\":0,\"declinedCount\":0,\"total\":0},\"open\":true},\"byInstanceType\":{}},\"build\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"failedBuildCount\":0,\"successfulBuildCount\":0,\"unknownBuildCount\":0},\"byInstanceType\":{}},\"review\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"stateCount\":0,\"state\":null,\"dueDate\":null,\"overDue\":false,\"completed\":false},\"byInstanceType\":{}},\"deployment-environment\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"topEnvironments\":[],\"showProjects\":false,\"successfulCount\":0},\"byInstanceType\":{}},\"repository\":{\"overall\":{\"count\":0,\"lastUpdated\":null},\"byInstanceType\":{}},\"branch\":{\"overall\":{\"count\":0,\"lastUpdated\":null},\"byInstanceType\":{}}}},\"isStale\":false}}",
      "aggregateprogress": {
        "progress": 0,
        "total": 0
      },
      "environment": null,
      "duedate": null,
      "progress": {
        "progress": 0,
        "total": 0
      },
      "comment": {
        "comments": [],
        "maxResults": 0,
        "total": 0,
        "startAt": 0
      },
      "votes": {
        "self": "http://localhost:9090/rest/api/2/issue/ES-24/votes",
        "votes": 0,
        "hasVoted": false
      },
      "worklog": {
        "startAt": 0,
        "maxResults": 20,
        "total": 0,
        "worklogs": []
      },
      "archivedby": null
    }
  }
}
```
</details> |
|  dev.cdevents.ticket.updated   | jira:issue_updated </br> jira:worklog_updated  |`jira:issue_updated` event type has various actions, issue_updated  issue_commented, issue_assigned
<details>
<summary>Event JSON issue_updated</summary>

```
{
  "timestamp": 1716992387526,
  "webhookEvent": "jira:issue_updated",
  "issue_event_type_name": "issue_updated",
  "user": {
    "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
    "name": "rjalander",
    "key": "JIRAUSER10000",
    "emailAddress": "jalander.ramagiri@est.tech",
    "avatarUrls": {
      "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
      "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
      "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
      "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
    },
    "displayName": "jalander.ramagiri@est.tech",
    "active": true,
    "timeZone": "Europe/Dublin"
  },
  "issue": {
    "id": "10023",
    "self": "http://localhost:9090/rest/api/2/issue/10023",
    "key": "ES-24",
    "fields": {
      "issuetype": {
        "self": "http://localhost:9090/rest/api/2/issuetype/10002",
        "id": "10002",
        "description": "Created by Jira Software - do not edit or delete. Issue type for a user story.",
        "iconUrl": "http://localhost:9090/images/icons/issuetypes/story.svg",
        "name": "Story",
        "subtask": false
      },
      "timespent": null,
      "project": {
        "self": "http://localhost:9090/rest/api/2/project/10000",
        "id": "10000",
        "key": "ES",
        "name": "EST-SeaTel",
        "projectTypeKey": "software",
        "avatarUrls": {
          "48x48": "http://localhost:9090/secure/projectavatar?avatarId=10324",
          "24x24": "http://localhost:9090/secure/projectavatar?size=small&avatarId=10324",
          "16x16": "http://localhost:9090/secure/projectavatar?size=xsmall&avatarId=10324",
          "32x32": "http://localhost:9090/secure/projectavatar?size=medium&avatarId=10324"
        }
      },
      "fixVersions": [],
      "customfield_10110": "0i00053:",
      "customfield_10111": null,
      "aggregatetimespent": null,
      "resolution": null,
      "customfield_10107": null,
      "customfield_10108": null,
      "customfield_10109": null,
      "resolutiondate": null,
      "workratio": -1,
      "lastViewed": "2024-05-29T15:14:18.184+0100",
      "watches": {
        "self": "http://localhost:9090/rest/api/2/issue/ES-24/watchers",
        "watchCount": 1,
        "isWatching": true
      },
      "created": "2024-05-29T15:04:18.022+0100",
      "priority": {
        "self": "http://localhost:9090/rest/api/2/priority/3",
        "iconUrl": "http://localhost:9090/images/icons/priorities/medium.svg",
        "name": "Medium",
        "id": "3"
      },
      "customfield_10100": null,
      "customfield_10101": null,
      "customfield_10102": null,
      "labels": [],
      "customfield_10103": null,
      "timeestimate": null,
      "aggregatetimeoriginalestimate": null,
      "versions": [],
      "issuelinks": [],
      "assignee": {
        "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
        "name": "rjalander",
        "key": "JIRAUSER10000",
        "emailAddress": "jalander.ramagiri@est.tech",
        "avatarUrls": {
          "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
          "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
          "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
          "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
        },
        "displayName": "jalander.ramagiri@est.tech",
        "active": true,
        "timeZone": "Europe/Dublin"
      },
      "updated": "2024-05-29T15:19:47.389+0100",
      "status": {
        "self": "http://localhost:9090/rest/api/2/status/10000",
        "description": "",
        "iconUrl": "http://localhost:9090/",
        "name": "To Do",
        "id": "10000",
        "statusCategory": {
          "self": "http://localhost:9090/rest/api/2/statuscategory/2",
          "id": 2,
          "key": "new",
          "colorName": "default",
          "name": "To Do"
        }
      },
      "components": [],
      "timeoriginalestimate": null,
      "description": "CDEvents integration with Jira updates needed",
      "timetracking": {},
      "archiveddate": null,
      "attachment": [],
      "aggregatetimeestimate": null,
      "summary": "CDEvents integration with Jira",
      "creator": {
        "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
        "name": "rjalander",
        "key": "JIRAUSER10000",
        "emailAddress": "jalander.ramagiri@est.tech",
        "avatarUrls": {
          "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
          "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
          "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
          "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
        },
        "displayName": "jalander.ramagiri@est.tech",
        "active": true,
        "timeZone": "Europe/Dublin"
      },
      "subtasks": [],
      "reporter": {
        "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
        "name": "rjalander",
        "key": "JIRAUSER10000",
        "emailAddress": "jalander.ramagiri@est.tech",
        "avatarUrls": {
          "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
          "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
          "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
          "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
        },
        "displayName": "jalander.ramagiri@est.tech",
        "active": true,
        "timeZone": "Europe/Dublin"
      },
      "customfield_10000": "{summaryBean=com.atlassian.jira.plugin.devstatus.rest.SummaryBean@314e1b0d[summary={pullrequest=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@2d06df[byInstanceType={},overall=PullRequestOverallBean{stateCount=0, state='OPEN', details=PullRequestOverallDetails{openCount=0, mergedCount=0, declinedCount=0}}], build=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@35d32094[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.BuildOverallBean@5d20d30f[failedBuildCount=0,successfulBuildCount=0,unknownBuildCount=0,count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], review=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@38ef0f2a[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.ReviewsOverallBean@6ae24cd6[dueDate=<null>,overDue=false,state=<null>,stateCount=0,count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], deployment-environment=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@4619169e[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.DeploymentOverallBean@1dfa0df9[showProjects=false,successfulCount=0,topEnvironments=[],count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], repository=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@5dacc733[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.CommitOverallBean@2550a4ac[count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], branch=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@2b73fb7e[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.BranchOverallBean@662bae2c[count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]]},configErrors=[],errors=[]], devSummaryJson={\"cachedValue\":{\"errors\":[],\"configErrors\":[],\"summary\":{\"pullrequest\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"stateCount\":0,\"state\":\"OPEN\",\"details\":{\"openCount\":0,\"mergedCount\":0,\"declinedCount\":0,\"total\":0},\"open\":true},\"byInstanceType\":{}},\"build\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"failedBuildCount\":0,\"successfulBuildCount\":0,\"unknownBuildCount\":0},\"byInstanparse error: Invalid numeric literal at line 1, column 8006
ceType\":{}},\"review\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"stateCount\":0,\"state\":null,\"dueDate\":null,\"overDue\":false,\"completed\":false},\"byInstanceType\":{}},\"deployment-environment\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"topEnvironments\":[],\"showProjects\":false,\"successfulCount\":0},\"byInstanceType\":{}},\"repository\":{\"overall\":{\"count\":0,\"lastUpdated\":null},\"byInstanceType\":{}},\"branch\":{\"overall\":{\"count\":0,\"lastUpdated\":null},\"byInstanceType\":{}}}},\"isStale\":false}}",
      "aggregateprogress": {
        "progress": 0,
        "total": 0
      },
      "environment": null,
      "duedate": null,
      "progress": {
        "progress": 0,
        "total": 0
      },
      "comment": {
        "comments": [],
        "maxResults": 0,
        "total": 0,
        "startAt": 0
      },
      "votes": {
        "self": "http://localhost:9090/rest/api/2/issue/ES-24/votes",
        "votes": 0,
        "hasVoted": false
      },
      "worklog": {
        "startAt": 0,
        "maxResults": 20,
        "total": 0,
        "worklogs": []
      },
      "archivedby": null
    }
  },
  "changelog": {
    "id": "10027",
    "items": [
      {
        "field": "description",
        "fieldtype": "jira",
        "from": null,
        "fromString": "CDEvents integration with Jira",
        "to": null,
        "toString": "CDEvents integration with Jira updates needed"
      }
    ]
  }
}
```
</details>
| | dev.cdevents.ticket.closed |   jira:issue_updated   | For ticket closed the type `issue_generic` will be created with the `resolution` field set to `Done` <details><summary>Event JSON issue_generic</summary>

```
{
  "timestamp": 1717165102467,
  "webhookEvent": "jira:issue_updated",
  "issue_event_type_name": "issue_generic",
  "user": {
    "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
    "name": "rjalander",
    "key": "JIRAUSER10000",
    "emailAddress": "jalander.ramagiri@est.tech",
    "avatarUrls": {
      "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
      "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
      "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
      "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
    },
    "displayName": "jalander.ramagiri@est.tech",
    "active": true,
    "timeZone": "Europe/Dublin"
  },
  "issue": {
    "id": "10008",
    "self": "http://localhost:9090/rest/api/2/issue/10008",
    "key": "ES-9",
    "fields": {
      "issuetype": {
        "self": "http://localhost:9090/rest/api/2/issuetype/10002",
        "id": "10002",
        "description": "Created by Jira Software - do not edit or delete. Issue type for a user story.",
        "iconUrl": "http://localhost:9090/images/icons/issuetypes/story.svg",
        "name": "Story",
        "subtask": false
      },
      "timespent": null,
      "project": {
        "self": "http://localhost:9090/rest/api/2/project/10000",
        "id": "10000",
        "key": "ES",
        "name": "EST-SeaTel",
        "projectTypeKey": "software",
        "avatarUrls": {
          "48x48": "http://localhost:9090/secure/projectavatar?avatarId=10324",
          "24x24": "http://localhost:9090/secure/projectavatar?size=small&avatarId=10324",
          "16x16": "http://localhost:9090/secure/projectavatar?size=xsmall&avatarId=10324",
          "32x32": "http://localhost:9090/secure/projectavatar?size=medium&avatarId=10324"
        }
      },
      "fixVersions": [],
      "customfield_10110": "0i0001r:",
      "customfield_10111": 3,
      "aggregatetimespent": null,
      "resolution": {
        "self": "http://localhost:9090/rest/api/2/resolution/10000",
        "id": "10000",
        "description": "Work has been completed on this issue.",
        "name": "Done"
      },
      "customfield_10107": null,
      "customfield_10108": null,
      "customfield_10109": null,
      "resolutiondate": "2024-05-31T15:18:22.446+0100",
      "workratio": -1,
      "lastViewed": "2024-05-31T15:18:22.419+0100",
      "watches": {
        "self": "http://localhost:9090/rest/api/2/issue/ES-9/watchers",
        "watchCount": 1,
        "isWatching": true
      },
      "created": "2024-05-29T14:18:38.402+0100",
      "priority": {
        "self": "http://localhost:9090/rest/api/2/priority/3",
        "iconUrl": "http://localhost:9090/images/icons/priorities/medium.svg",
        "name": "Medium",
        "id": "3"
      },
      "customfield_10100": null,
      "customfield_10101": null,
      "customfield_10102": null,
      "labels": [],
      "customfield_10103": null,
      "timeestimate": null,
      "aggregatetimeoriginalestimate": null,
      "versions": [],
      "issuelinks": [],
      "assignee": null,
      "updated": "2024-05-31T15:18:22.450+0100",
      "status": {
        "self": "http://localhost:9090/rest/api/2/status/10001",
        "description": "",
        "iconUrl": "http://localhost:9090/",
        "name": "Done",
        "id": "10001",
        "statusCategory": {
          "self": "http://localhost:9090/rest/api/2/statuscategory/3",
          "id": 3,
          "key": "done",
          "colorName": "success",
          "name": "Done"
        }
      },
      "components": [],
      "timeoriginalestimate": null,
      "description": null,
      "timetracking": {},
      "archiveddate": null,
      "attachment": [],
      "aggregatetimeestimate": null,
      "summary": "As a developer, I'd like to update story status during the sprint >> Click the Active sprints link at the top right of the screen to go to the Active sprints where the current Sprint's items can be updated",
      "creator": {
        "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
        "name": "rjalander",
        "key": "JIRAUSER10000",
        "emailAddress": "jalander.ramagiri@est.tech",
        "avatarUrls": {
          "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
          "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
          "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
          "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
        },
        "displayName": "jalander.ramagiri@est.tech",
        "active": true,
        "timeZone": "Europe/Dublin"
      },
      "subtasks": [],
      "reporter": {
        "self": "http://localhost:9090/rest/api/2/user?username=rjalander",
        "name": "rjalander",
        "key": "JIRAUSER10000",
        "emailAddress": "jalander.ramagiri@est.tech",
        "avatarUrls": {
          "48x48": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=48",
          "24x24": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=24",
          "16x16": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=16",
          "32x32": "https://www.gravatar.com/avatar/acc35d47cafd5f3edca6b0f6db7f3921?d=mm&s=32"
        },
        "displayName": "jalander.ramagiri@est.tech",
        "active": true,
        "timeZone": "Europe/Dublin"
      },
      "customfield_10000": "{summaryBean=com.atlassian.jira.plugin.devstatus.rest.SummaryBean@368b0950[summary={pullrequest=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@57d89d90[byInstanceType={},overall=PullRequestOverallBean{stateCount=0, state='OPEN', details=PullRequestOverallDetails{openCount=0, mergedCount=0, declinedCount=0}}], build=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@6fd95e24[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.BuildOverallBean@7c7e6a52[failedBuildCount=0,successfulBuildCount=0,unknownBuildCount=0,count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], review=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@47d13bf4[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.ReviewsOverallBean@76206dc3[dueDate=<null>,overDue=false,state=<null>,stateCount=0,count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], deployment-environment=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@532d355d[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.DeploymentOverallBean@5c8ee990[showProjects=false,successfulCount=0,topEnvironments=[],count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], repository=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@12ce676e[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.CommitOverallBean@67f54e81[count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]], branch=com.atlassian.jira.plugin.devstatus.rest.SummaryItemBean@5d4808ff[byInstanceType={},overall=com.atlassian.jira.plugin.devstatus.summary.beans.BranchOverallBean@7621b8af[count=0,lastUpdated=<null>,lastUpdatedTimestamp=<null>]]},configErrors=[],errors=[]], devSummaryJson={\"cachedValue\":{\"errors\":[],\"configErrors\":[],\"summary\":{\"pullrequest\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"stateCount\":0,\"state\":\"OPEN\",\"details\":{\"openCount\":0,\"mergedCount\":0,\"declinedCount\":0,\"total\":0},\"open\":true},\"byInstanceType\":{}},\"build\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"failedBuildCount\":0,\"successfulBuildCount\":0,\"unknownBuildCount\":0},\"byInstanceType\":{}},\"review\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"stateCount\":0,\"state\":null,\"dueDate\":null,\"overDue\":false,\"completed\":false},\"byInstanceType\":{}},\"deployment-environment\":{\"overall\":{\"count\":0,\"lastUpdated\":null,\"topEnvironments\":[],\"showProjects\":false,\"successfulCount\":0},\"byInstanceType\":{}},\"repository\":{\"overall\":{\"count\":0,\"lastUpdated\":null},\"byInstanceType\":{}},\"branch\":{\"overall\":{\"count\":0,\"lastUpdated\":null},\"byInstanceType\":{}}}},\"isStale\":false}}",
      "aggregateprogress": {
        "progress": 0,
        "total": 0
      },
      "environment": null,
      "duedate": null,
      "progress": {
        "progress": 0,
        "total": 0
      },
      "comment": {
        "comments": [],
        "maxResults": 0,
        "total": 0,
        "startAt": 0
      },
      "votes": {
        "self": "http://localhost:9090/rest/api/2/issue/ES-9/votes",
        "votes": 0,
        "hasVoted": false
      },
      "worklog": {
        "startAt": 0,
        "maxResults": 20,
        "total": 0,
        "worklogs": []
      },
      "archivedby": null
    }
  },
  "changelog": {
    "id": "10104",
    "items": [
      {
        "field": "resolution",
        "fieldtype": "jira",
        "from": null,
        "fromString": null,
        "to": "10000",
        "toString": "Done"
      },
      {
        "field": "status",
        "fieldtype": "jira",
        "from": "10000",
        "fromString": "To Do",
        "to": "10001",
        "toString": "Done"
      }
    ]
  }
}
```
</details> |

Note:

CDEvents do not have corresponding mapping with Jira Project related, User related, Configuration and Software related events, this needs a discussion on how to handle these Jira events.
Various Jira event types can be found at https://developer.atlassian.com/server/jira/platform/webhooks/#configuring-a-webhook.


