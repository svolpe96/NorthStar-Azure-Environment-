# NorthStar Azure Enterprise Environment

This is the Azure side of my [Physical Environment](https://github.com/svolpe96/NorthStar-Enterprise-Lab), a physical environment I built using Cisco networking, Proxmox, Windows Server, and Active Directory.

I'm using Azure to expand on what I've already built and get hands-on with with cloud networking, administration, identity, security, and eventually hybrid infrastructure.

## What I'm Building

I'm planning to build two Azure network designs and document both.

### 1. Single VNet

I'll start with one VNet divided into subnets for different workloads. This will be a working environment where I can deploy VMs, configure NSGs and routing, manage access, and test connectivity and security.

### 2. Hub-and-Spoke

Once the single-VNet design is built and tested, I'll move to hub-and-spoke. I want to learn VNet peering, shared connectivity, and how to separate workloads across multiple VNets.

The reason I chose to do both is to get experience with each design and the process of moving from one to the other. I'll keep the documentation and test results from the first build even after moving to the second. I'll plan workload migration carefully so I don't unnecessarily lose data or configurations.

## Planned Expansion

- Microsoft Entra ID and hybrid identity with my existing `north.local` domain
- Private connectivity between Azure and NorthStar on-premises
- Azure-hosted domain controller and file services
- Backup and restore testing
- Azure Monitor and Microsoft Sentinel
- Security controls, governance, and infrastructure as code

## Current Status

**Planning:** No Azure resources have been confirmed as deployed yet. I'm starting with the network design, naming conventions, IP addressing, and cost controls.

I'm targeting roughly **$30–$50 per month**, so I'll run VMs when needed and evaluate ongoing costs before deploying services.

As the project progresses, I'll add architecture diagrams, configurations, screenshots, validation, and troubleshooting notes in separate project folders instead of putting every technical detail in this README.
