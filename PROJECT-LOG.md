# NorthStar Azure Project Log

This is my running log of what I worked on, decisions I made, and issues I ran into. Detailed documentation lives in the project folders.

## October 16, 2026

### Corrected the Azure budget

I found that my original `budget-northstar-monthly` was created with an annual reset period, even though I intended a monthly budget. I deleted it and recreated it with a monthly reset, a $50 amount, and an expiration date of October 1, 2028. I configured actual-cost email alerts at 40% ($20), 70% ($35), and 90% ($45), without action groups. The Budgets page now shows the budget as Monthly with $0.00 evaluated spend. The budget provides alerts, not a hard spending cap.

## October 15, 2026

### Created the Azure subscription

I created `sub-northstar-prod-01` with the Microsoft Azure Plan, using my existing directory and billing account. It didn't appear in the Subscriptions list immediately, but showed up later.

### Planned the network layout

I chose East US and planned a single VNet (`172.20.0.0/20`) with Servers, Management, Applications, and Security subnets. I included Security so I can eventually test Splunk and subnet isolation alongside Microsoft Sentinel. I also reserved address ranges for a later hub-and-spoke design. None of the network resources have been deployed yet.

I chose separate resource groups for networking, compute, identity, storage, and monitoring. See [Initial Azure Design](01-Architecture/initial-design.md) for the full plan.

### Cost Management issue

I attempted to configure a $50 monthly budget with alerts at $20, $35, and $45. Azure displayed "Unable to load some of the filter values" and "Cannot load data," and the budget form wasn't editable. I'll retry later. The budget is not confirmed active.
