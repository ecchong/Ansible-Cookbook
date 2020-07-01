## Setup Tower notification for MS Team

https://github.com/ansible/awx/issues/885

- In MS Team channel, go to More Options -> Connectors.  Configure "Incoming Webhook".  Assign a name and create.
- Copy the generated URL.
- Create a Tower Notification using Mattermost type.  Paste the Team Webhook URL into TARGET URL