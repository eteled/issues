#eteled

GitHub bot to actively delete comments for a closed thread (issue, commit, pull request).

Simple Usage Instructions:

1. Add @eteled to your repo collaborators (So it can delete comments)
2. Put a comment saying "@eteled START" (capitalization important) on the issue/PR.
3. @eteled will delete all future comments on that thread as they are created. (It also makes a comment notifying that all future comments will be deleted)

![eteled](https://f.cloud.github.com/assets/584253/1665353/385f6838-5c36-11e3-9e65-f226d56ad0bb.png)


You can check a sample at captn3m0/github-image-post#1. It allows the issue/PR to be referenced from another issue, as @isaacs asked for. To re-enable comments on the issue, you can comment "@eteled STOP".

It runs using a webhook for inbound emails on its email address (using postmarkapp.com). Each email is sent via a webhook to the app running on Heroku. Depending on the notification, it decides individually to delete/skip the comment and watch/unwatch the thread.

**Limitations**

- Its currently running on the postmark free tier, so it will stop working after it processes 10k emails. 
- It cannot stop watchers from receiving notifications or replying to them via email. So, the comments may be visible for a small time (~2 minutes) before they are deleted.

File any issues/bugs/feature-requests [here](https://github.com/eteled/issues/issues/new)


Test commit.
