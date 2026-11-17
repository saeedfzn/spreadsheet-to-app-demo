# Spreadsheet to app: a Power Platform concept demo

**Live demo:** https://saeedfzn.github.io/spreadsheet-to-app-demo/

Lots of teams track something in a shared spreadsheet and chase approvals by email. This demo shows how I'd replace one of those spreadsheets, using purchase requests as the example. It covers four pieces:

1. **A simple app**: one validated form instead of free-text cells, plus an approver view. It blocks duplicates and bad values.
2. **Automations**: four flows covering routing to the right approver (Finance as well for anything over £500), telling the requester the decision, a daily digest of overdue items and a Monday summary.
3. **A live dashboard**: approved spend by department, requests per week, items overdue and average time to decide, with department and date filters.
4. **Where AI fits next**: a Copilot Studio agent for "where's my request?", AI category suggestions and Copilot summaries in Power BI. These are proposed next steps and aren't built in this page.

## What this is (and isn't)

It's an interactive concept in plain HTML and JavaScript (`index.html`, no build step, no dependencies). All the data is made up. That way anyone can click through it without a Microsoft 365 licence.

In a real Microsoft 365 tenancy the same design would be built like this:

| Demo piece | Real build |
|---|---|
| Request form and approver view | Power Apps canvas app (Power Fx) |
| Requests data | SharePoint Lists: `Requests`, `Departments`, `Categories` |
| Flow run log | Power Automate cloud flows on the standard SharePoint and Office 365 Outlook connectors |
| Dashboard | Power BI report over the Requests list |
| AI ideas | Copilot Studio agent in Teams, AI Builder prompt, Copilot in Power BI |

## Design notes for the real build

- **Data model.**
  - `Requests` has Item, Department (lookup), Category (choice), Cost, Requester (person), Status (choice), Approver (person), Submitted and Decided.
  - `Departments` has Name, Approver and Budget.
  - `Categories` has Name and the threshold above which Finance must also approve.
- **Delegation.** Index Status and Submitted, and filter on them, so the app stays correct past the 2,000-row limit.
- **Permissions.** Requesters see their own items, approvers see their department, and admins see everything. Nobody can approve their own request.
- **Edge cases to test.** Duplicate submissions, a department with no approver, spend over the limit, self-approval, and a request edited after it was approved.
- **Handover.** A short user guide and an admin guide, so the team can run it without me.

## About me

I'm Faizaan Saeed, a Power Platform and AI automation developer based in Swindon. I've delivered a real system on this stack: a stock-control system for a manufacturer, with a Power Apps app on SharePoint Lists, six Power Automate flows, automatic Excel reports and an in-app dashboard. It was delivered in 15 days and signed off. [LinkedIn](https://www.linkedin.com/in/faizaan-saeed-ba96a426b)

Microsoft, Power Apps, Power Automate, Power BI, SharePoint and Copilot are trademarks of Microsoft. This is an independent demo.
