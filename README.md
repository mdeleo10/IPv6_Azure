# IPv6 Support in Azure
What services support IPv6

Azure Portal - Dual Stacked?
Azure CLI - No ?

Infrastructure

| Infrastructure  | Supported |
| ------------- | ------------- |
| VNET (Virtual Networks) | Yes, Dual Stack  |
| Subnets | Yes, Dual Stack |
| NAT Gateway | Yes? |
| Public IP | Yes |
| NIC  | Yes, Dual Stack (must have IPv4) |
| Private Endpoints | No |
| Private Links | No |
| VPN Gateway | No |
| ExpressRoute Gateway | Yes, Dual Stack |
| Internal Load Balancer | |
| External Load Balancer | |
| Application Gateway | No |
| FrontEnd | ??? |
| DDOS | ??? |


Platform as a Service
| PaaS  | Supported |
| ------------- | ------------- |
| Azure Active Directory | Yes | See https://learn.microsoft.com/en-us/troubleshoot/azure/active-directory/azure-ad-ipv6-support |
| Azure DNS | 
| AKS | ?? |
