# Auth0 - Logs to Application Insights Webtask

A webtask that will take all of your Auth0 logs and export them to Application Insights.

## Configure Application Insights

First you'll need an Application Insights account which you can create for free in your [Azure Subscription](https://portal.azure.com/#create/Microsoft.AppInsights).

## Configure Webtask

If you haven't configured Webtask on your machine run this first:

```
npm i -g wt-cli
wt init
```

> Requires at least node 0.10.40 - if you're running multiple version of node make sure to load the right version, e.g. "nvm use 0.10.40"

## Deployment

If you just want to run it once:

```
wt create https://raw.githubusercontent.com/sandrinodimattia/auth0-logs-to-appinsights-webtask/master/task.js \
    --name auth0-logs-to-appinsights \
    --secret AUTH0_DOMAIN={YOUR_AUTH0_DOMAIN} \
    --secret AUTH0_GLOBAL_CLIENT_ID={YOUR_AUTH0_GLOBAL_CLIENT_ID} \
    --secret AUTH0_GLOBAL_CLIENT_SECRET={YOUR_AUTH0_GLOBAL_CLIENT_SECRET} \
    --secret APPINSIGHTS_INSTRUMENTATIONKEY=9c812656-5950-4de5-a34d-391774691855
```

If you want to run it on a schedule (run every 5 minutes for example):

```
wt cron schedule \
    --name auth0-logs-to-appinsights \
    --secret AUTH0_DOMAIN={YOUR_AUTH0_DOMAIN} \
    --secret AUTH0_GLOBAL_CLIENT_ID={YOUR_AUTH0_GLOBAL_CLIENT_ID} \
    --secret AUTH0_GLOBAL_CLIENT_SECRET={YOUR_AUTH0_GLOBAL_CLIENT_SECRET} \
    --secret APPINSIGHTS_INSTRUMENTATIONKEY=9c812656-5950-4de5-a34d-391774691855 \
    --json \
    "*/5 * * * *" \
    https://raw.githubusercontent.com/sandrinodimattia/auth0-logs-to-appinsights/master-webtask/task.js
```

> You can get your Global Client Id/Secret here: https://auth0.com/docs/api/v1

## Usage

Now go to the [Azure Portal](https://portal.azure.com/) and you'll see Errors and Custom Events showing up.
