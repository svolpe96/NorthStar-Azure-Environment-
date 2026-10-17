# Initial Azure Design

This is the plan I settled on before deploying NorthStar's Azure infrastructure. I wanted to work through the addressing and resource layout first so I wouldn't have to undo things later, especially when I start connecting Azure to my physical lab.

## Subscription and region

- Subscription: `sub-northstar-prod-01` — **created and visible in Azure**
- Initial region: **East US** (`eus`)
- Billing: Microsoft Azure Plan
- Monthly spending target: **$30–$50**
- Budget name: `budget-northstar-monthly` — **created, $50 monthly**

I initially created the budget with an annual reset by mistake, then deleted and recreated it with a monthly reset. The actual-cost alerts are $20 (40%), $35 (70%), and $45 (90%). These alerts do not enforce a hard spending cap. See [Cost Management](../02-Governance/Cost-Management.md).

I plan to deallocate VMs when I'm not using them and watch for services that keep charging even when the VMs are stopped.

## Naming convention

I'm using lowercase, hyphen-separated names where Azure supports them, generally:

`<resource-type>-<workload>-<environment>-<region>-<instance>`

The `prod` label means *simulated production* within this lab, not an actual production business.

Examples:

- `rg-network-prod-eus-01`
- `vnet-northstar-prod-eus-01`
- `nsg-servers-prod-eus-01`

## Version 1: Single VNet (deployed; security configuration pending)

My on-premises networks use `10.0.x.0/24` ranges, so I chose a separate Azure address allocation: `172.20.0.0/16`. This leaves room for future Azure VNets without overlapping my current on-premises ranges.

Initial VNet: **`vnet-northstar-prod-eus-01` — `172.20.0.0/20`**

| Subnet | Address range | Intended use | Planned NSG |
| --- | --- | --- | --- |
| `snet-servers` | `172.20.1.0/24` | Domain controller and file services | `nsg-servers-prod-eus-01` |
| `snet-management` | `172.20.2.0/24` | Administrative workloads | `nsg-management-prod-eus-01` |
| `snet-applications` | `172.20.3.0/24` | Web and application workloads | `nsg-applications-prod-eus-01` |
| `snet-security` | `172.20.4.0/24` | Self-hosted security tools and testing | `nsg-security-prod-eus-01` |

I decided to include a Security subnet from the beginning, even if it stays empty initially. Microsoft Sentinel doesn't need a subnet, but I may deploy Splunk temporarily to practice log ingestion, SPL, and security monitoring. Keeping a separate subnet also gives me another segment to secure and test with NSGs.

I deployed the VNet and all four subnets. I removed the default subnet, enabled the private subnet option (no default outbound access), and left NAT gateways, NSGs, and route tables unassigned for now. NSG rules and routing still need to be configured and tested. The deployment details are in [Virtual Network](../03-Networking/Virtual-Network.md).

## Version 2: Hub-and-spoke (future design)

I've reserved the following non-overlapping ranges for a possible second architecture:

| Network | Reserved address range | Intended role |
| --- | --- | --- |
| Original single VNet | `172.20.0.0/20` | Version 1 |
| Hub | `172.20.16.0/20` | Shared connectivity |
| Identity spoke | `172.20.32.0/20` | Identity services |
| Application spoke | `172.20.48.0/20` | Applications |
| Security spoke | `172.20.64.0/20` | Security workloads |

These are planning reservations, not deployed VNets. I'll revisit the sizing and workload migration approach when I actually build hub-and-spoke. I want to preserve documentation and test results from both architectures.

## Resource groups

| Resource group | Purpose |
| --- | --- |
| `rg-network-prod-eus-01` | VNets, NSGs, route tables — **created** |
| `rg-compute-prod-eus-01` | General-purpose VMs |
| `rg-identity-prod-eus-01` | Domain controllers and identity-related infrastructure |
| `rg-storage-prod-eus-01` | Storage and file services |
| `rg-monitoring-prod-eus-01` | Log Analytics, Sentinel, and monitoring |

I chose to keep identity separate from general compute because I plan to add an Azure domain controller and hybrid identity later. I'll create these groups as they're needed.

I applied these tags to the networking resource group: `Project=NorthStar`, `Environment=Prod-Lab`, `Owner=Steven`, and `Purpose=Networking`. Tags don't automatically inherit from a subscription to every resource, so I'll apply them as appropriate.

## Next steps

1. Configure subnet NSGs and the rules needed for the workloads.
2. Deploy test workloads when ready and verify connectivity and segmentation.
3. Document the results and any issues I run into.
