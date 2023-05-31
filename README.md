# IPv6 Support in Azure
Is there IPv6 support in Azure? Yes. Most Infrastructure as a Service, but not many Platform as a Service. No native IPv6 only networking is supported yet.

## Pricing

There's **no charge** to use Public IPv6 Addresses or Public IPv6 Prefixes. Associated resources and bandwidth are charged at the same rates as IPv4.

## Is the Azure Portal Dual Stacked?
Yes, the https://portal.azure.com site is dual-stacked, https://portal.azure.us is not. But the Azure cli doesn't seem to support IPv6. Azure Powershell to be confirmed.

 

## Infrastructure (IaaS)

| Service  | Supported | Reference | Notes | 
| ------------- | ------------- | ------------- | ------------- | 
| Azure Public IP address prefixes | Yes - Used for VMs, Standard Load Balancers, Azure Firewall, VPN Gw* | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/public-ip-address-prefix |
| VNET (Virtual Networks) | Yes, Dual Stack  | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview |
| Subnets | Yes, Dual Stack and must be exactly /64 | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview |
| VNET peering | Yes | https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-peering-overview | 
| Azure Virtual WAN | No | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview | Azure Virtual WAN currently supports IPv4 traffic only. |
| Network Security Groups (NSG) | Yes | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview | ICMPv6 isn't currently supported in Network Security Groups. |
| User Defined Routes (UDR) | yes | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview |
| DHCPv6 for Linux VMs (some need manual config) | Yes | https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-ipv6-for-linux?tabs=ubuntu | 
| NAT Gateway | No | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/configure-public-ip-nat-gateway | Public IPv6 address and public IPv6 prefixes aren't supported on NAT gateways at this time. However, NAT gateways can be deployed on a dual stack virtual network subnet with IPv6 and IPv4 prefixes. | 
| Public IP | Yes | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/public-ip-addresses | support DNS Name Label | 
| NIC  | Yes, Dual Stack (must have IPv4) | |
| Azure Firewall | No | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview | Azure Firewall doesn't currently support IPv6. It can operate in a dual stack VNet using only IPv4, but the firewall subnet must be IPv4-only. |
| Private Endpoints | No | |
| Private Links | No | |
| VPN Gateway | No | |
| ExpressRoute Gateway | Yes, Dual Stack | |
| Standard Internal Load Balancer | Yes | https://learn.microsoft.com/en-us/azure/load-balancer/ipv6-dual-stack-standard-internal-load-balancer-powershell |
| Standard Public Load Balancer | Yes | https://learn.microsoft.com/en-us/azure/load-balancer/virtual-network-ipv4-ipv6-dual-stack-standard-load-balancer-powershell |
| Application Gateway v2 | No | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview | Application Gateway v2 doesn't currently support IPv6. It can operate in a dual stack virtual network using only IPv4, but the gateway subnet must be IPv4-only. Application Gateway v1 doesn't support dual stack virtual networks. |
| FrontEnd | ??? | |
| Bastion | No | | |
| DDOS | Yes | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview |
| IPv6 Troubleshooting and Diagnostics are available with load balancer metrics/alerting and Network Watcher features such as packet capture, NSG flow logs, connection troubleshooting and connection monitoring. | Yes | |

Limitations, see https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview

The current IPv6 for Azure Virtual Network release has the following limitations:
* VPN gateways currently support IPv4 traffic only, but they still can be deployed in a dual-stacked virtual network using Azure PowerShell and Azure CLI commands only.
* Dual-stack configurations that use floating IP can only be used with public load balancers, not internal load balancers.
* Application Gateway v2 doesn't currently support IPv6. It can operate in a dual stack virtual network using only IPv4, but the gateway subnet must be IPv4-only. Application Gateway v1 doesn't support dual stack virtual networks.
* The Azure platform (AKS, etc.) doesn't support IPv6 communication for Containers.
* IPv6-only Virtual Machines or Virtual Machines Scale Sets aren't supported, each NIC must include at least one IPv4 IP configuration.
* To add IPv6 to existing IPv4 deployments, you can't add IPv6 ranges to a virtual network that has existing resource navigation links.
* While it's possible to create NSG rules for IPv4 and IPv6 within the same NSG, it isn't currently possible to combine an IPv4 subnet with an IPv6 subnet in the same rule when specifying IP prefixes.
* ICMPv6 isn't currently supported in Network Security Groups.
* Azure Virtual WAN currently supports IPv4 traffic only.
* Azure Firewall doesn't currently support IPv6. It can operate in a dual stack VNet using only IPv4, but the firewall subnet must be IPv4-only.

Note: In my experience, deploying Marketplace solutions may not properly deploy on dual-stacked subnets.

Creating a dual-stacked VM - Note that *INTERNAL* IPv6 NIC address is address-translated to the Public IPv6 address for inbound and outbound Internet access. Remember that NAT-GW is not supported yet, so only one Public IP address is translated. If scalability is required, see Load Balancer as an option.
- Azure Portal - https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/create-vm-dual-stack-ipv6-portal
- Azure CLI - https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/create-vm-dual-stack-ipv6-cli 
- Azure Powershell - https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/create-vm-dual-stack-ipv6-powershell 


## Platform as a Service (PaaS)
| Service  | Supported | Reference | Notes |
| ------------- | ------------- | ------------- | ------------- | 
| Azure Active Directory | Yes | See https://learn.microsoft.com/en-us/troubleshoot/azure/active-directory/azure-ad-ipv6-support |
| Azure DNS - Azure DNS support for IPv6 (AAAA) records, no inverse resolution* | | | Forward DNS for IPv6 is supported for Azure public DNS. Reverse DNS isn't supporte | 
| AKS | Yes with limitations | [https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview](https://learn.microsoft.com/en-us/azure/aks/configure-kubenet-dual-stack?tabs=azure-cli%2Ckubectl) | See page for more details |
| Managed SQL | ?? | |
| App Services | ?? | |

## Software as a Service (SaaS)

| Service  | Supported | Reference | Notes |
| ------------- | ------------- | ------------- | ------------- | 
| Microsoft Azure Active Directory | Phased approach |  https://techcommunity.microsoft.com/t5/microsoft-entra-azure-ad-blog/ipv6-coming-to-azure-ad/ba-p/2967451 | |
| Microsoft Exchange Online (supports IPv6) | Yes | https://learn.microsoft.com/en-us/microsoft-365/enterprise/ipv6-support?view=o365-worldwide |  |
| Microsoft SharePoint Online (Can be enabled with IPv6 with a support request) | | | 
| Microsoft Teams (Only supports IPv4) | | | 


