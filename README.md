# NorthStar Azure Enterprise Environment

This repository is where I'm documenting the Azure side of my NorthStar environment. I already have an on-premises setup with Cisco networking, Proxmox, Active Directory, and Windows servers. My goal is to extend that environment into Azure and get more hands-on experience with cloud administration, networking, identity, security, backup, and monitoring.

This is a personal lab designed to simulate an enterprise environment, not an actual production business. I want to follow realistic design practices while keeping the cost manageable.

My existing on-premises project is documented here: [NorthStar Enterprise Lab](https://github.com/svolpe96/NorthStar-Enterprise-Lab).

## Architecture plan

I've decided to build and document **two Azure network architectures**, one after the other.

### Version 1 — Single VNet

I'll start by building a functional Azure environment using a single VNet with separate subnets for servers, management, and applications.

The plan is to work through resource groups, addressing, NSGs, routing, Azure RBAC, virtual machines, storage, and connectivity/security testing. I'll use actual workloads where they make sense, rather than deploying resources just for screenshots.

This will be the first working version of NorthStar Azure, not just a temporary diagram.

### Version 2 — Hub-and-spoke

After building, testing, and documenting the single-VNet environment, I'll design and deploy a separate hub-and-spoke architecture.

The hub will eventually provide shared connectivity, including a potential connection to my on-premises NorthStar network. Spokes will separate workloads such as identity, applications, and security/monitoring.

I want to practice VNet peering, routing, isolation, and troubleshooting, then migrate or redeploy the appropriate workloads from Version 1. Before changing anything, I'll work out which resources can stay, which need to move, and which might need to be recreated. The goal is to preserve data and configurations where practical, not delete everything and start over.

I'll keep the diagrams, configuration notes, screenshots, and validation results for **both** versions in this repository, even after the first architecture is retired. I don't plan to keep two complete environments running indefinitely.

## Hybrid integration goals

Longer term, I want Azure to become part of the existing NorthStar environment rather than an unrelated cloud setup.

Planned areas to explore include:

- Microsoft Entra hybrid identity synchronization with my existing `north.local` Active Directory
- Private connectivity between Azure and the on-premises New York site
- A second domain controller in Azure, with AD DS/DNS replication and testing
- File services, off-site backups, and actual restore testing
- Azure Monitor, Log Analytics, Splunk, and eventually Microsoft Sentinel
- Azure security, governance, and infrastructure as code

Entra identity synchronization and network-level hybrid connectivity are separate pieces of this project. I'll work on the Azure foundation first and revisit the site-to-site VPN options when I need them. A managed VPN Gateway and a self-managed VPN solution are both options to evaluate based on cost, security, and what I want to learn.

## Initial design decisions

| Area | Current plan |
| --- | --- |
| Azure subscription | `sub-northstar-prod-01` (chosen name; deployment status not yet verified) |
| Subscription model | Pay-As-You-Go |
| Naming | Lowercase, hyphenated names where supported; `prod` represents simulated production |
| Region | East US (`eus`) proposed |
| Azure address space | `172.20.0.0/16` reserved as the overall planning range; individual VNet ranges still to be finalized |
| First architecture | Single VNet with separate subnets |
| Second architecture | Hub-and-spoke, after Version 1 is validated |
| Budget | Target around $30–$40/month, with approximately $50/month as the upper goal |
| VM usage | Primarily on demand; deallocate when not in use |

These are design decisions and proposals, **not claims that the Azure resources have already been deployed**.

## Cost approach

I'm keeping this environment on a small personal budget. Before deploying resources, I'll check both their expected running costs and any charges that continue when they're stopped. I plan to configure Azure Cost Management budgets and alerts at $20, $35, and $45. Those alerts are notifications, not automatic spending limits.

I'll avoid leaving expensive networking services or VMs running continuously unless there's a reason to do so.

## Documentation approach

I'll document what I actually configured, tested, broke, fixed, and learned. That includes architecture diagrams, relevant settings and commands, screenshots, validation results, and troubleshooting notes.

I want this repository to show the progression from a working single-VNet design to a hub-and-spoke design, including the reasons for the change and what it took to get there.

## Current status

**Planning / design.** The architecture sequence has been decided, but I haven't confirmed any Azure resources as deployed yet. Next steps are to finalize naming, IP addressing, subnet design, estimated costs, and cost controls before building Version 1.
