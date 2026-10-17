# Azure Cost Management

I set up a subscription-level budget before deploying any Azure infrastructure so I can keep track of what the NorthStar lab costs as I build it.

## Budget configuration

<img width="1711" height="909" alt="image" src="https://github.com/user-attachments/assets/1071cfcc-72bb-433f-ab1c-c376b5a3815e" />



The budget alerts me as spending increases, but it does **not** stop resources or cap charges at $50. My plan is to keep the lab around $30–$50 per month, shut down/deallocate VMs when I'm not using them, and watch for charges that continue while VMs are stopped, such as disks and other provisioned services.

## What I ran into

I originally created the budget with an **annual** reset period by mistake. The Azure Cost Management page also initially had loading issues, including errors about filter values and cost data. Once the portal was working, I found the annual budget, deleted it, and recreated `budget-northstar-monthly` with the correct monthly reset period.

I verified the new budget on the Azure Budgets page on October 16, 2026. It showed **Monthly**, **$50.00**, and **$0.00 evaluated spend** at that point. The three alert thresholds were also visible on the budget details page.

