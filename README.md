#eteled

Eteled is a github bot that auto-deletes any future comments from a GitHub discussion (issue/commit/PR).

##History
eteled was born [from a discussion](https://github.com/isaacs/github/issues/38) where people wanted a "no more comments" button for a repository. This would be helpful in cases where a discussion thread devolved into a "mess of trolls".

##How does it work
eteled uses a webhook on postmarkapp to deliever all mail to a webhook (powered by Sinatra+Heroku). All requests made to `/webhook` are parsed by eteled, and appropriately responded to. Depending on the notification, it decides individually to delete/skip the comment or watch/unwatch the thread. It uses `jsonblob.com` as its backend for storing the list.

##Simple Usage Instructions:

1. Add @eteled to your repo collaborators (So it can delete comments). 
2. Put a comment saying "@eteled START" (capitalization important) on the issue/PR. (The user must be a collaborator himself in order for this command to take effect).
3. @eteled will delete all future comments on that thread as they are created. (It also makes a comment notifying that all future comments will be deleted)

![eteled](https://f.cloud.github.com/assets/584253/1665353/385f6838-5c36-11e3-9e65-f226d56ad0bb.png)

##Limitations

- Its currently running on the postmark free tier, so it will stop working after it processes 10k emails. 
- It cannot stop watchers from receiving notifications or replying to them via email. So, the comments may be visible for a small time (~2 minutes) before they are deleted.

##Development
In case your development machine is not on the internet (thus cannot receive a webjhook), use [ngrok](https://ngrok.com/) and tunnel all requests to the
port at which your sinatra app is running (default=9393/5000).  
You can use the following three variables in a file called `.env` to
change the configuration options:

1. `OAUTH_TOKEN` - Required. Generate from github settings.
2. `JSONBLOB_URL` - Required. A valid JSONBlob.com blob URL (Something like `http://jsonblob.com/api/jsonBlob/:hash`)
3. `OCTOKIT_API_ENDPOINT` - Optional. Use this to test eteled against a GitHub enterprise or developer setup. I use it to proxy all eteled requests in development through `runscope.net`, an excellent tool to debug API Requests.

##Licence
Licenced under the MIT Licence.

File any issues/bugs/feature-requests [here](https://github.com/eteled/issues/issues/new)
