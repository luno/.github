# GitHub Copilot Licence Management System

This document explains how the automated GitHub Copilot licence management system works for the Luno organisation.

## System Overview

The automated system manages GitHub Copilot licences by:

- ✅ **Daily monitoring** of Copilot licence usage (every day at 9am UTC)
- ✅ **Automatic reminders** for users who haven't used Copilot for **14+ days**
- ✅ **Licence revocation** for users inactive for **30+ days**
- ✅ **Issue tracking** with assignments to inactive users
- ✅ **Automatic issue closure** when users become active again
- ✅ **Duplicate prevention** to avoid multiple reminders for the same user

## System Components

The system consists of several integrated components working together:

### Required Infrastructure

- **Label**: `copilot-reminder` - Used to tag and track reminder issues
- **Repository Secret**: `COPILOT_UPDATE_TOKEN` - Personal access token used by the workflow
- **Repository Variable**: `COPILOT_REMINDER_MESSAGE` - Stores the reminder message template
- **GitHub Actions Workflow**: Automates the entire process daily

## Workflow Process

The automated workflow operates on a daily schedule and follows this process:

### Daily Execution

**Schedule**: Every day at 9am UTC via GitHub Actions cron schedule  
**Manual Trigger**: Available through the "Run workflow" button in Actions tab

### Reminder Message Content

The system uses a standardised message template *stored in a repository variable*:

```markdown
## 🤖 GitHub Copilot Licence Reminder

Hi there! 👋

We noticed you haven't used your assigned licence for **GitHub Copilot** and it has been inactive for a period of 14 days. Here are some resources that might help you get started:

### 🚀 Getting Started
* **Setup Guide**: If you haven't yet set up Copilot in your environment, see [Setting up GitHub Copilot for yourself](https://docs.github.com/en/copilot/setting-up-github-copilot/setting-up-github-copilot-for-yourself)
* **Troubleshooting**: Having issues? Check [Troubleshooting common issues with GitHub Copilot](https://docs.github.com/en/copilot/troubleshooting-github-copilot/troubleshooting-common-issues-with-github-copilot)
* **Luno-specific tips**: Check out the bookmarks in our #engineering-with-ai channel

### 📚 Best Practices & Tips
* **Best Practices**: Learn how to get the most out of Copilot with [Best practices for using GitHub Copilot](https://docs.github.com/en/copilot/using-github-copilot/best-practices-for-using-github-copilot)
* **Prompt Engineering**: Improve your prompts with [Prompt engineering for GitHub Copilot](https://docs.github.com/en/copilot/using-github-copilot/prompt-engineering-for-github-copilot)
* **Examples**: See practical examples in the [Copilot Chat Cookbook](https://docs.github.com/en/copilot/example-prompts-for-github-copilot-chat)

### 💬 Need Help?
If you're having trouble getting started or have questions about using Copilot effectively, feel free to:
- Comment on this issue
- Reach out to your team lead
- Ask in our internal development channels

### ⚡ Next Steps
If you no longer need access to GitHub Copilot, please let us know in this issue. If your licence remains inactive for a further 16 days (30 total), we'll revoke it to free up access for another user.

---
*This is an automated reminder sent daily to help ensure our Copilot licences are being used effectively.*
```

## System Logic & Automation

### Timing Thresholds

The system operates on a two-stage approach:

- **14 days inactive**: First reminder issue created with helpful resources and 16-day warning
- **30 days inactive**: Licence automatically revoked and reminder issue closed
- **Schedule**: Runs every day at 9am UTC via GitHub Actions
- **Manual trigger**: Available through the "Run workflow" button
- **Auto-closure**: Issues are automatically closed when users become active again

### Issue Management Process

The system manages GitHub issues with the following behaviour:

**Issue Creation (14 days inactive):**

- Creates issues with title: "Reminder about your GitHub Copilot licence"
- Assigns issues directly to the inactive user
- Tags issues with the `copilot-reminder` label
- Includes comprehensive setup and troubleshooting resources
- Warns users about licence revocation in 16 days

**Duplicate Prevention:**

- Checks for existing open issues with the `copilot-reminder` label
- Skips users who already have an active reminder issue
- Prevents notification spam for the same user

**Automatic Issue Closure:**

- **When users become active**: Issues are closed with a celebratory comment
- **When licences are revoked**: Issues are closed with a revocation notice
- Maintains a clean issue tracker with current status

## User Journey Examples

### Scenario 1: User Becomes Active

- **Day 1**: User gets assigned Copilot licence
- **Day 14**: User hasn't used licence → Reminder issue created with 16-day warning
- **Day 18**: User starts using Copilot → Issue automatically closed with celebration message

### Scenario 2: Licence Revocation

- **Day 1**: User gets assigned Copilot licence  
- **Day 14**: User hasn't used licence → Reminder issue created with 16-day warning
- **Day 30**: User still hasn't used licence → Licence revoked, issue closed with notice

**Workflow Logs:**

- Detailed execution logs available in **Actions** → workflow run → job details
- Visual indicators: ✅ (active), ⚠️ (inactive), ℹ️ (already reminded)
- Timestamp tracking for all API calls and decisions
