# 📘 SCM, Polling & Webhooks with Jenkins Setup

------------------------------------------------------------------------

# 🔹 1. Source Code Management (SCM)

## 📌 Definition

SCM manages and tracks code changes.

## 🛠️ Example (Git)

    git init
    git add .
    git commit -m "Initial commit"

------------------------------------------------------------------------

# 🔹 2. Polling

## 📌 Definition

Client repeatedly checks server for updates.

## 🔧 Jenkins Poll SCM Setup

1.  Open Jenkins Dashboard
2.  Go to Job → Configure
3.  Scroll to **Build Triggers**
4.  Select **Poll SCM**
5.  Add cron:

```{=html}
<!-- -->
```
    H/5 * * * *

6.  Save

------------------------------------------------------------------------

# 🔹 3. Webhooks

## 📌 Definition

Server sends data when event occurs.

------------------------------------------------------------------------

# 🔧 GitHub Webhook Setup

## Steps:

1.  Go to GitHub repo
2.  Click **Settings**
3.  Click **Webhooks**
4.  Click **Add Webhook**
5.  Payload URL:

```{=html}
<!-- -->
```
    http://<jenkins-url>/github-webhook/

6.  Content type: application/json
7.  Select: Just push event
8.  Save

------------------------------------------------------------------------

# 🔧 Jenkins Webhook Setup

## Steps:

1.  Install plugin:
    -   GitHub Integration Plugin
2.  Go to Job → Configure
3.  Select:
    -   ✅ GitHub hook trigger for GITScm polling
4.  Save

------------------------------------------------------------------------

# 🔹 4. Polling vs Webhooks

  Feature      Polling    Webhooks
  ------------ ---------- -------------
  Speed        Slow       Instant
  Calls        Repeated   Event-based
  Efficiency   Low        High

------------------------------------------------------------------------

# 🎯 Interview One-Liner

Polling checks repeatedly, webhooks trigger instantly on events.
