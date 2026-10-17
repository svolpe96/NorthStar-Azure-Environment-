# Virtual Network

I created `vnet-northstar-prod-eus-01` in East US under `rg-network-prod-eus-01`. This is the first version of my Azure network. I wanted to start with a single VNet, get the networking and security working, and then build a hub-and-spoke design later so I can compare both approaches.

I used `172.20.0.0/20` because my physical NorthStar environment uses `10.0.x.x` networks. Keeping the ranges separate will make it easier to connect the two environments later without overlapping addresses.

## Subnets

I removed the default subnet Azure created and added four `/24` subnets:

- `snet-servers` — `172.20.1.0/24`: server workloads, including a possible Azure domain controller.
- `snet-management` — `172.20.2.0/24`: administration and troubleshooting.
- `snet-applications` — `172.20.3.0/24`: application and web workloads.
- `snet-security` — `172.20.4.0/24`: security tools and network isolation testing.

I enabled the private subnet setting, which means the subnets don't get default outbound internet access. I left NAT gateways, network security groups, and route tables unassigned while creating the VNet. I'll configure and test NSGs separately as the next part of the project.

I also left Azure Bastion, Azure Firewall, and the other optional VNet security features disabled for now because I want to keep this lab within my $50 monthly budget.

## Screenshot

I captured the VNet address space page showing all four subnets during setup. I'll add that screenshot here once it's uploaded to GitHub.

## Next

Configure NSGs and test traffic between subnets once I have workloads available. The VNet and subnets are deployed; the security rules and connectivity tests aren't done yet.
