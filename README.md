# IPv6 Support in Azure
What services support IPv6

Azure Portal - Dual Stacked?
Azure CLI - No ?

Infrastructure (IaaS)

| Service  | Supported | Reference |
| ------------- | ------------- | ------------- | 
| VNET (Virtual Networks) | Yes, Dual Stack  | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview |
| Subnets | Yes, Dual Stack and must be exactly /64 | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview |
| Network Security Groups (NSG) | Yes | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview |
| User Defined Routes (UDR) | yes | https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/ipv6-overview |
| DHCPv6 for Linux VMs (some need manual config) | Yes | https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-ipv6-for-linux?tabs=ubuntu | 
| NAT Gateway | Yes? | |
| Public IP | Yes | | (via NAT GW)
| NIC  | Yes, Dual Stack (must have IPv4) | |
| Private Endpoints | No | |
| Private Links | No | |
| VPN Gateway | No | |
| ExpressRoute Gateway | Yes, Dual Stack | |
| Internal Load Balancer | | |
| Standard Load Balancer | Yes | https://learn.microsoft.com/en-us/azure/load-balancer/virtual-network-ipv4-ipv6-dual-stack-standard-load-balancer-powershell |
| Application Gateway | No | |
| FrontEnd | ??? | |
| DDOS | ??? | |


Platform as a Service (PaaS
| Service  | Supported | Reference |
| ------------- | ------------- | ------------- | 
| Azure Active Directory | Yes | See https://learn.microsoft.com/en-us/troubleshoot/azure/active-directory/azure-ad-ipv6-support |
| Azure DNS | | |
| AKS | ?? | |
| Managed SQL | ?? | |
| App Services | ?? | |


