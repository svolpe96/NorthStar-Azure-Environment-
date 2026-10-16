# NorthStar Azure Enterprise Environment

This is the Azure side of my [Physical Environment](https://github.com/svolpe96/NorthStar-Enterprise-Lab), where I've been working with Cisco networking, Proxmox, Windows Server, and Active Directory.

I'm using Azure to expand the lab and get hands-on experience with cloud networking, administration, identity, security, and eventually hybrid infrastructure. This is a simulated enterprise environment, not a production business.

## What I'm Building

### 1. Single VNet

I'm starting with one VNet and separate subnets for servers, management, applications, and security. I'll configure and test connectivity, NSGs, routing, and workloads as I build it.

### 2. Hub-and-Spoke

After testing the single-VNet design, I'll build a hub-and-spoke architecture to learn peering, shared connectivity, and workload separation. I want to document both designs and the transition between them rather than skip straight to the final architecture.

## Planned Expansion

- Microsoft Entra ID and hybrid identity with my existing `north.local` domain
- Private connectivity to the physical NorthStar environment
- Azure-hosted domain controller and file services
- Backup and restore testing
- Azure Monitor, Microsoft Sentinel, and hands-on Splunk testing
- Security controls, governance, and infrastructure as code

## Current Status

**Subscription created; infrastructure not yet deployed.** I've selected East US for the initial design and planned the VNet, subnets, resource groups, and naming conventions. The $50 monthly budget setup is pending while Azure Cost Management finishes loading.

I'm aiming to keep the lab around **$30–$50 per month**, running VMs only when needed.

See [01-Architecture / Initial Azure Design](01-Architecture/initial-design.md) for the addressing plan, resource organization, and current setup status. I'll add actual configurations, screenshots, testing, and troubleshooting as I build.
