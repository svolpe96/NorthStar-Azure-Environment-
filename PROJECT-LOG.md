# NorthStar Azure Project Log

This is my running log of what I worked on, decisions I made, and issues I ran into. Detailed documentation lives in the project folders.

## October 15, 2026

I created `sub-northstar-prod-01` with the Microsoft Azure Plan, using my existing directory and billing account. It didn't appear in the Subscriptions list immediately, but showed up later.

I chose East US and planned a single VNet (`172.20.0.0/20`) with Servers, Management, Applications, and Security subnets. I included Security so I can eventually test Splunk and subnet isolation alongside Microsoft Sentinel. I also reserved address ranges for a later hub-and-spoke design. None of the network resources have been deployed yet.

I chose separate resource groups for networking, compute, identity, storage, and monitoring. See [Initial Azure Design](01-Architecture/initial-design.md) for the full plan.

I attempted to configure a $50 monthly budget with alerts at $20, $35, and $45. Azure displayed "Unable to load some of the filter values" and "Cannot load data," and the budget form wasn't editable. I'll retry later. The budget is not confirmed active.
