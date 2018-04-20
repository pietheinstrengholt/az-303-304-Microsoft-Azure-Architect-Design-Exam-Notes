# 70-535-Architecting-Microsoft-Azure-Solutions-Exam-Notes

### Azure Geos and Regions
- 42 regions globally
- Geos: East US, Canada Central, North Europe.
- Each region has a pair for highest-speed connections and highest availability.

### Azure Virtual Networks
- IP Addresses: Difference between public and private. Dynamic assigned. You can point DNS using CNAME records. Static IP, allows A records to be set. SSL security. Useful for firewall settings. 4096 Private IP's per Vnet. 60 Public dynamic IP's, 20 Status public IP's
- Network Security Groups (NSGs): can contain list of ACL rules. Allow or denies access to resources based on priority. Associated with vnets, subnets, vm's. When Associated with a subnet the ACL is applied on that subnet. Can only be applied within a region.
Resource groups: Allows to operate on a group of resources. Allows access control, billing, in-group communication. Resource can only be part of one group. No nesting is allowed. You can link however. No limits. Unable to rename after creation.

### Azure Compute
- Azure Compute: Azure App Service (web apps, mobile apps, logic apps, api apps)
- Web Apps: Shared or dedicated virtual machines, managed, any language, ASP.net, NodeJS, PHP or Python. Powershell as scripting. CI/CD capabilities and security options.
- Mobile Apps: Supports any language with the Azure SDK. Supports single sign on via Azure AD FS. Build offline ready apps. Supports push notifications. Supports staging environments.
- API Apps: Easy migrate existing API's, CORS, Access control and supports integration with Logic Apps. Logic Apps: Build workflows. Trigger based (If this then that), causes actions to happen. Works with templates. Can be created in the browser.
- Virtual Machines: Virtual Machines which come in many different flavors and types.

### VPN & Express Route
- P2S Point-to-Site VPN: VPN connection for single connection or single computer. Useful for development or debugging. Uses the Public Internet. 
- S2S Site-toSite VPN: VPN connection for multiple computers. Requires a Gateway. Network is secure encrypted. Not suited for huge amount of traffic. Uses the Public Internet and speed is limited. Up to 200mbs speed.
- ExpressRoute: Enterprise dedicated connection. Not via the internet. Up to 10GB speed. Offers dedicated servers for for storage, backup, and recovery, as if it runs in your own data center.

### Azure Services & Solutions:
- Azure Load Balancer: Load Balancer to balance the web traffic. Checks with 15 seconds interval is servers are still alive.
- Internal Load Balancer: Load Balancer to balance internal traffic. Allows different ports and security configuration options.
- Azure Application Gateway: Gateway that has a WAF (Web Application Firewall) to inspect traffic. Is able to perform robin traffic. Allows Secure Sockets Layer-offload (SSL). Can route traffic based on content inspection.
- Traffic Manager: Manages and balances the load between different regions.
- Azure Media Services: Does encoding and decoding of media. Useful for websites that work with video and video-streaming content.
- Azure Content Delivery Network (CDN): Serves out static content from much faster locations.
- Azure Active Directory: Identity management
- Microsoft Azure Redis Cache: Caching engine using Redis. Useful for frequently accessed content or sessions.
- Azure Multi-Factor Authentication: Additional Authentication with mobile phone (sms), mobile app or telephone call
- Azure Service Bus: message queue which can be used to decouple applications.

### Managed Identities
- Azure AD: Multi-tentant, which means it facilitates groups of users with common access rights. Typically used together with SaaS. Enables and allows Single Sign On (SSO) to any cloud or on prem app. Has a Free, Basic and Premium plan.
- IDMaaS: Identity Management as a Service.
- Graph API: Rest API to authenticate. Works with a token and time intervals.
- OAuth & OpenID: uses the open standards for authentication. User does not have to provide username and password to Azure. 3rd party takes care of this.

### Hybrid Identities
- Hybrid entities: Mixure of cloud and on prem network. Allows one identity regardless where the apps are hosted.
- SAML Claims: Security Assertions Markup Language. SAML tokens are called claims. SAML tokens are signed.
- Azure AD FS: Federated Identities. Responsibility is turned over to a 3rd party.
- AD Application Proxy: SSO for remote employee to access web applications hosted inside. No need to have a VPN. Authentication through the proxy. 

### Network Security Group
- Network Security Group is a virtual firewall. Uses inbound and outbound rules. NSG can be associated to multiple NIC's or subnets. Each NIC or subnet only uses one NSG. Default; only allows outbound. No inbound.
- Data security in transit and at rest: SSL/TLS (Https). For at rest the Azure Storage Service Encryption (SSE) is used. 256-bit AES. ARM only. For Block blobs, page blobs and append blobs. Client side encryption is possible as well. Azure Disk Encryption = Encrypt the disks used by Virtual Machines.
- Azure Operations Management Suite: A Suite to monitor traffic, see unusual things, etc.

