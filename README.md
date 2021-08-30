# Azure Solutions Architect Expert exam notes

Useful websites:
- Microsoft Learn: https://docs.microsoft.com/en-us/learn/
- Azure documentation: https://docs.microsoft.com/en-us/azure/
- Azure Architecture Center: https://docs.microsoft.com/en-us/azure/architecture/
- Azure 303 Exam site: https://docs.microsoft.com/en-us/learn/certifications/exams/az-303
- Azure 304 Exam site: https://docs.microsoft.com/en-us/learn/certifications/exams/az-304
- Azure Quickstart Templates: https://github.com/Azure/azure-quickstart-templates
- Azure Governance Docs: https://docs.microsoft.com/en-us/azure/governance/
- Cloud Adoption Framework: https://azure.microsoft.com/en-us/cloud-adoption-framework/
- Azure Well Architected Framework: https://docs.microsoft.com/en-us/azure/architecture/framework/
- Azure Resource Explorer: http://resources.azure.com/
- Azure Shell: http://shell.azure.com/

### Architect and Design Identity and Security

- Azure subscription: An Azure subscription is a logical container used to provision resources in Azure. It holds the details of all your resources like virtual machines (VMs), databases, and more. 
    - A subscription is associated with a *single* Azure AD directory.
        - Subscriptions in Azure are both a billing entity and a security boundary. Microsoft rolls up all the resources in a subscription and sends a single bill for the entire subscription. There is no ability to sub define payment information below the subscription level.
    - Azure subscriptions can only trust a single directory, but multiple subscriptions can be associated to a single Azure AD instance.
    - One or more Azure subscriptions can establish a trust relationship with an instance of Azure Active Directory (Azure AD) in order to authenticate and authorize security principals and devices against Azure services.
    - Virtual Networks cannot span across subscriptions.
    - Multiple subscriptions can roll up to an Azure Enterprise Agreement (Azure EA)

- Azure Active Directory: Azure Active Directory (Azure AD) is Microsoft's enterprise cloud-based identity and access management (IAM) solution.
    - Users and groups can be added to multiple subscriptions - this allows the user to create, control, and access resources in the subscription.
    - Azure AD defines users in three ways:
        - Cloud identities - These users exist only in Azure AD. Examples are administrator accounts and users that you manage yourself.
        - Directory-synchronized identities - These users exist in an on-premises Active Directory. 
        - Guest users - These users exist outside Azure.
    - Azure AD allows you to define two different types of groups:
        - Security groups. These are the most common and are used to manage member and computer access to shared resources for a group of users.
        - Microsoft 365 groups. These groups provide collaboration opportunities by giving members access to a shared mailbox, calendar, files, SharePoint site, and more.
    - Three role types:
        - Owner, which has full access to all resources, including the right to delegate access to others.
        - Contributor, which can create and manage all types of Azure resources but can’t grant access to others.
        - Reader, which can view existing Azure resources.
    - A role definition is a collection of permissions. A role definition lists the operations that can be performed, such as read, write, and delete.
        - A role can be assigned to a special type of group. In order to do so you must create the group with the role assignment flag set to true.
    - You can tailor the Actions and NotActions properties to grant and deny the exact permissions you need. 
    - Data operations are specified in the DataActions and NotDataActions properties.
    - The AssignableScopes property of the role specifies the scopes (subscriptions, resource groups, or resources) within which the role is available for assignment.
    - Different user roles:
        - Administrator roles in Azure AD allow users elevated access to control who is allowed to do what.
        - A member user account is a native member of the Azure AD organization that has a set of default permissions like being able to manage their profile information. When someone new joins your organization, they typically have this type of account created for them.
        - Guest users have restricted Azure AD organization permissions. When you invite someone to collaborate with your organization, you add them to your Azure AD organization as a guest user.
    - Role-based access control (RBAC) for Azure resources: Use RBAC roles to manage access to Azure resources like virtual machines, SQL databases, or storage. For example, you could assign an RBAC role to a user to manage and delete SQL databases in a specific resource group or subscription.
    - There are different ways you can assign access rights:
        - Direct assignment: Assign a user the required access rights by directly assigning a role that has those access rights.
        - Group assignment: Assign a group the required access rights, and members of the group will inherit those rights.
        - Rule-based assignment: Use rules to determine a group membership based on user or device properties. For a user account or device's group membership to be valid, the user or device must meet the rules. If the rules aren't met, the user account or device's group membership is no longer valid. The rules can be simple. You can select prewritten rules or write your own advanced rules.
    - Administrative Units: An administrative unit is an Azure AD resource that can be a container for other Azure AD resources. An administrative unit can contain only users and groups. Administrative units restrict permissions in a role to any portion of your organization that you define.
    - Azure Active Directory B2B: With Azure Active Directory (Azure AD) business to business (B2B), you can add people from other companies to your Azure AD tenant as guest users. 
        - The partner typically has the responsibility to manage its own identities. External users continue to use their current identities to collaborate with your organization.
    - Authentication in Azure Active Directory. Users authenticate in two stages:
        - The identity provider verifies the identity of users who exist in the directory. Upon successful authentication, tokens are issued that contain information related to the successful authentication.
        - The user passes those tokens to the application. The application must validate the user’s security tokens to ensure that authentication was successful.
    - OAuth 2.0 is the industry-standard protocol for authorization. It provides specific authorization flows for web, desktop, and mobile applications. This specification was primarily designed to enable users to authorize an application to access data in another application.
    - OpenID Connect is an authentication layer that's built on top of OAuth 2.0. It includes identity verification methods that are missing from OAuth 2.0. OpenID Connect gives you an access token plus an ID token, which you can send to an application to prove your identity. The ID token is a JSON Web Token (JWT) and contains information about the authenticated user. The identity provider signs the token, so that applications can verify the authentication by using the provider's public key.
    - Azure AD Multi-Factor Authentication (MFA) supplies added security for your identities by requiring two or more elements for full authentication. These elements fall into three categories:
        - Something you know - which might be a password or the answer to a security question.
        - Something you possess - which might be a mobile app that receives a notification or a token-generating device.
        - Something you are - which typically is a biometric property, such as a fingerprint or face scan used on many mobile devices.
    - Device identity in Azure Active Directory (Azure AD) helps you control the devices that you add to your organization's Azure AD instance. You have three device registration options to add a device to Azure AD:
        - Azure AD registered: These devices fall into the Bring Your Own Device (BYOD) category. They're typically privately owned, or they use a personal Microsoft account or another local account. 
        - Azure AD joined: These devices are owned by your organization. Users access your cloud-based Azure AD instance through their work account. Device identities exist only in the cloud. With Azure AD join, you can join devices to your Azure Active Directory organization without needing to sync with an on-premises Active Directory instance. Azure AD join is best suited to organizations that are principally cloud based, although it can operate in a hybrid cloud and on-premises environment.
        - Hybrid Azure AD joined: This option is similar to Azure AD joined. The devices are owned by the organization, and they're signed in with an Azure AD account that belongs to that organization. Device identities exist in the cloud and on-premises.
    - Conditional access in Azure AD uses data from sources known as signals, validates them against a user-definable rule base, and chooses the best outcome to enforce your organization's security policies. Conditional access enables device identity management, but conditional access policies can be complex.
        - Conditional Access policies are enforced after first-factor authentication is completed.
    - Enterprise State Roaming: Enterprise State Roaming enables users of Windows 10 devices to sync settings and application data with their organization's cloud service.
    - Self-service password reset (SSPR): With SSPR, users can reset their passwords in a web browser or from a Windows sign-in screen to regain access to Azure, Microsoft 365, and any other application that uses Azure AD for authentication.
    - Custom domain names: You can add up to 900 managed domain names to your Azure AD organization. Azure provides the default domain name onmicrosoft.com to all Azure AD organizations. You're free to use it in your organization to create users and grant them access to resources. If your company chooses this approach, your users sign in with username@something.onmicrosoft.com.
    - Azure AD supports three options for hybrid identies: https://docs.microsoft.com/en-us/azure/active-directory/hybrid/choose-ad-authn
        - Password hash synchronization + Seamless SSO: Password Single Sign-On Uses the user’s account information from the third-party SaaS application. With this approach, the user’s account information and password is collected, securely stored in Azure AD, and provided to the SaaS application via a web browser extension.
        - Pass-through Authentication + Seamless SSO: Azure AD Single Sign-On Uses the user’s account information directly from Azure AD. If the user is already signed into Azure AD (or Office 365), there is no need for the user to reauthenticate when accessing the third-party SaaS application. A limited number of applications in the Azure AD application gallery support federation-based SSO.
        - Federation with AD FS: Existing Single Sign-On Uses an existing Active Directory Federation Services (AD FS) or other third-party provider for SSO.
    - Azure AAD Portal: with https://aad.portal.azure.com/, it only shows you azure ad for your tenant and only allows managing resources in Azure AD (users, groups, devices, enterprise apps, security logs, etc.)

- Azure AD Application Proxy: Application Proxy enables users to leverage SSO to securely access on-premises web applications such as SharePoint sites and Outlook Web Access—without the need for building or maintaining a VPN or complicated network infrastructure.

- Azure Active Directory Privileged Identity Management (PIM): Privileged Identity Management (PIM) is a service in Azure Active Directory (Azure AD) that enables you to manage, control, and monitor access to important resources in your organization. These resources include resources in Azure AD, Azure, and other Microsoft Online Services such as Microsoft 365 or Microsoft Intune. Identity Protection uses adaptive machine learning algorithms and heuristics to detect anomalies and risk events that may indicate that an identity has been compromised.
    - Azure PIM only applies to administrative roles within Azure

- Azure AD Domain Services: Domain Services provide fully managed domain services such as domain join, group policy, LDAP, Kerberos/NTLM, and so on that are compatible with Windows Server Active Directory. This features enables you to use these services without the need to build and manage Azure virtual machines (VMs) running Windows Server Active Directory or maintain a site-to-site VPN connection between Azure and your on-premises directory infrastructure.

- Azure AD Device Registration: Azure AD Device Registration is an Azure AD feature that enables mobile devices (such as iOS, Android, and Windows devices) to be registered in Azure AD. The registered device, and thus attributes of the device, can be used to enable conditional access to on-premises or Office 365 applications.

- Azure AD Cloud App Discovery: Cloud App Discovery enables IT departments to discover cloud applications used in their organization, thus allowing the applications to be brought under IT control to help mitigate risk of potential data leakage or other security threats. Cloud App Discovery finds the applications being used (including various usage metrics), identifies users, and enables offline data analysis. Cloud App Discovery is a feature of Azure AD Premium.

- Azure AD Connect Health: Azure AD Connect Health enables you to monitor and gain insights into the overall health of the integration between your on-premises Windows Server Active Directory/Active Directory Federation Service and Azure AD (or Office 365).

- Azure AD Identity Protection: Azure AD Identity Protection is a security service that enables you to gain insights into potential security vulnerabilities affecting users in your organization (more specifically, their identities). For example, Identity Protection can use knowledge of leaked credentials (hash codes) or sign-ins from geographic locations to which it would be impossible to travel (that is, time between sign-ins is less than the time needed to travel to the different locations).

- Azure AD Connect: Azure AD Connect is the Microsoft tool designed to meet and accomplish your hybrid identity goals.
    - This is a free tool you can download and install to synchronize your local AD with your Azure directory.
    - Active Directory Federation Services (AD FS): Federation is an optional part of Azure AD Connect that you can use to configure a hybrid environment via an on-premises AD FS infrastructure. Organizations can use this to address complex deployments, such as domain join SSO, enforcement of the Active Directory sign-in policy, and smart card or third-party multi-factor authentication.
    - Password hash synchronization. This feature is a sign-in method that synchronizes a hash of a user’s on-premises Active Directory password with Azure AD.
    - Pass-through authentication. This allows users to sign in to both on-premises and cloud-based applications using the same passwords. This reduces IT helpdesk costs because users are less likely to forget how to sign in. This feature provides an alternative to Password hash synchronization that allows organizations to enforce their security and password complexity policies.

- Microsoft Identity: Microsoft identity platform is an evolution of the Azure Active Directory (Azure AD) developer platform.
    - Microsoft identity includes three solutions for addressing the largest number of users:
        - Azure Active Directory (Azure AD)
        - Azure AD business to business (B2B) enables an organization in Azure AD to securely share files and resources with another organization in Azure AD.
        - Azure AD Business to Customer (B2C) enables an organization to provide customer-facing apps that enable users to sign with an identity they already have, such as a Microsoft Account, Gmail, Facebook, or Twitter account or create an account for the solution. Azure AD B2C is primarily for businesses and developers that create customer-facing apps. 
    - Microsoft Graph is the gateway to all your data in the Microsoft Cloud. From Office 365, Enterprise Mobility + Security to Windows 10, Microsoft Graph enables developers to build applications that provide users access to their data. Developers and users can access their data with Microsoft Graph by authenticating and authorizing users with Microsoft identity.
    - OpenID Connect extends the OAuth 2.0 authorization protocol to use as an authentication protocol, so that you can implement single sign-on using OAuth in your applications. It also introduces the concept of an ID token.
    - Access tokens enable clients to securely call APIs protected by Azure AD. Applications should never inspect or validate an access token. Access tokens must only be passed to the API.
        - The easiest way to use Microsoft identity for authentication and to obtain access tokens to authorize requests to secured endpoints in SPAs is to use the Microsoft Authentication Library (MSAL) for JavaScript.
    - Conditional Access enables enterprise customers to protect services in a multitude of ways including multi-factor authentication, allowing only Intune-enrolled devices to access specific services, and restricting user locations and IP ranges.
    - Single Tenant Apps: Applications that sign in users only from the app’s home tenant are called single tenant applications.
    - Multi-Tenant Apps: The other type of application is one that allows users from more than just your organization to sign in and use the application. These applications can also allow users to sign in using their personal Microsoft account.
    - When you register an Azure AD application in the Azure portal, two objects are created in your Azure AD tenant:
        - Application object: The Application object is where developers specify how the app works. This includes parameters for authentication, secrets, or certificates, what permissions the app will use, any APIs the app exposes.
        - Service principal object: An Azure service principal is an identity created for use with applications, hosted services, and automated tools to access Azure resources. This access is restricted by the roles assigned to the service principal, giving you control over which resources can be accessed and at which level. IT Pros use the Service Principal to determine how the application operates within their tenant. The IT PRO can limit the app to specific users and/or groups, review permissions and grant consent, assign users and/or groups to roles, or configure app provisioning. More info: https://docs.microsoft.com/en-us/azure/active-directory/develop/app-objects-and-service-principals
        - There are three types of service principal: application, managed identity, and legacy.
            - Application: This service principal is the local representation, or application instance, of a global application object in a single tenant or directory. In this case, a service principal is a concrete instance created from the application object and inherits certain properties from that application object. A service principal is created in each tenant where the application is used and references the globally unique app object. The service principal object defines what the app can actually do in the specific tenant, who can access the app, and what resources the app can access.
            - Managed identity: Managed identities eliminate the need for developers to manage credentials. Managed identities provide an identity for applications to use when connecting to resources that support Azure AD authentication. When a managed identity is enabled, a service principal representing that managed identity is created in your tenant. Service principals representing managed identities can be granted access and permissions, but cannot be updated or modified directly.
            - Legacy: The third type of service principal represents a legacy app (an app created before app registrations were introduced or created through legacy experiences). A legacy service principal can have credentials, service principal names, reply URLs, and other properties which are editable by an authorized user, but does not have an associated app registration. The service principal can only be used in the tenant where it was created.

- Azure management groups: Azure management groups provide a level of scope above subscriptions. You organize subscriptions into containers called "management groups" and apply your governance conditions to the management groups. All subscriptions within a management group automatically inherit the conditions applied to the management group.
    - Up to 6 levels deep. Each child can only have one parent.
    - By default, the root management group's display name is Tenant root group.
    - Inherit Policies, RBAC permissions and Budgets. So a child receives any permissions from its parent. For example, if on root group a policy is set that certain Virtual Machines SKUs are not allowed, then all underlying mamagement groups and subscriptions will inherit this policy.s

### Architect network infrastructure in Azure

Azure region: An Azure region is a set of datacenters, deployed within a latency-defined perimeter and connected through a dedicated regional low-latency network. With more global regions than any other cloud provider, Azure gives customers the flexibility to deploy applications where they need.
    - A regional pair consists of two regions within the same geography. Azure serializes platform updates (planned maintenance) across regional pairs, ensuring that only one region in each pair updates at a time. If an outage affects multiple regions, at least one region in each pair will be prioritized for recovery. More info: https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions

- Availability zones: Availability Zones are unique physical locations within an Azure region. Each zone is made up of one or more datacenters with independent power, cooling, and networking. The physical separation of Availability Zones within a region limits the impact to applications and data from zone failures, such as large-scale flooding, major storms and superstorms, and other events that could disrupt site access, safe passage, extended utilities uptime, and the availability of resources.
    - With zonal architecture, a resource can be deployed to a specific, self-selected Availability Zone to achieve more stringent latency or performance requirements. Resiliency is self-architected by replicating applications and data to one or more zones within the region.
    - With zone-redundant architecture, the Azure platform automatically replicates the resource and data across zones. Microsoft manages the delivery of high availability, since Azure automatically replicates and distributes instances within the region.
    - Latest zonal (Z) and zone-redundant (ZR) Azure services can be found here: https://docs.microsoft.com/en-us/azure/architecture/high-availability/building-solutions-for-high-availability

- Virtual networks: A virtual network is a virtual, isolated portion of the Azure public network. Each virtual network is dedicated to your subscription.
    - You can create multiple virtual networks per subscription and per region. You can create multiple subnets within each virtual network.
    - Each virtual network that you connect to another virtual network, or on-premises network, must have a unique address space. Each virtual network has one or more public or private address ranges assigned to its address space. An address range is specified in classless internet domain routing (CIDR) format, such as 10.0.0.0/16.
    - A network interface enables a VM to communicate with other resources. Each network interface has one or more private IP addresses assigned to it.
    - If you connect virtual networks, you can implement a network virtual appliance, such as a firewall, to control the flow of traffic between the virtual networks.
    - When you set up a VNet, you specify the topology, including the available address spaces and subnets. If the VNet is to be connected to other VNets or on-premises networks, you must select address ranges that don't overlap.
    - The IP addresses are private and can't be accessed from the Internet, which was true only for the non-routable IP addresses such as 10.0.0.0/8, 172.16.0.0/12, or 192.168.0.0/16.
    - Virtual Machines:
        - VMs can be created in the same VNet and they can connect to each other using private IP addresses. They can connect even if they are in different subnets without the need to configure a gateway or use public IP addresses. To put VMs into a VNet, you create the VNet and then as you create each VM, you assign it to the VNet and subnet. VMs acquire their network settings during deployment or startup.
        - VMs are assigned an IP address when they are deployed. If you deploy multiple VMs into a VNet or subnet, they are assigned IP addresses as they boot up. You can also allocate a static IP to a VM. If you allocate a static IP, you should consider using a specific subnet to avoid accidentally reusing a static IP for another VM.
        - If you create a VM and later want to migrate it into a VNet, it is not a simple configuration change. You must redeploy the VM into the VNet.
    - VNet Integration: VNet Integration gives your app access to resources in your VNet, but it doesn't grant inbound private access to your app from the VNet. Private site access refers to making an app accessible only from a private network, such as from within an Azure virtual network. VNet Integration is used only to make outbound calls from your app into your VNet. The VNet Integration feature behaves differently when it's used with VNet in the same region and with VNet in other regions. The VNet Integration feature has two variations:
        - Regional VNet Integration: When you connect to Azure Resource Manager virtual networks in the same region, you must have a dedicated subnet in the VNet you're integrating with.
        - Gateway-required VNet Integration: Gateway-required VNet Integration provides access to resources only in the target VNet or in networks connected to the target VNet with peering or VPNs. Gateway-required VNet Integration doesn't enable access to resources available across Azure ExpressRoute connections or work with service endpoints. 
        - More info: https://docs.microsoft.com/en-us/azure/app-service/web-sites-integrate-with-vnet
    - Virtual Network NAT: Virtual Network NAT (network address translation) simplifies outbound-only Internet connectivity for virtual networks. When configured on a subnet, all outbound connectivity uses your specified static public IP addresses.
    - Route table: Azure automatically routes traffic between Azure subnets, virtual networks, and on-premises networks. If you want to change any of Azure's default routing, you do so by creating a route table.

- Subnets: A subnet is a range of IP addresses in the VNet. You can divide a VNet into multiple subnets for organization and security.
    - Each NIC in a VM is connected to one subnet in one VNet. 
    - NICs connected to subnets (same or different) within a VNet can communicate with each other without any extra configuration.
    - By default, there is no security boundary between subnets, so VMs in each of these subnets can talk to one another.
    - You can set up Network Security Groups (NSGs), which allow you to control the traffic flow to and from subnets and to and from VMs.

- Network security groups: filter network traffic to and from Azure resources. A network security group (NSG) contains a list of Access Control List (ACL) rules that allow or deny network traffic to subnets, NICs, or both.
    - Filters traffic between VMs or subnets.
    - NSGs contain two sets of rules: inbound and outbound.
    - All NSGs contain a set of default rules. The default rules cannot be deleted, but because they are assigned the lowest priority, they can be overridden by the rules that you create.
    - When an NSG is associated with a subnet, the ACL rules apply to all the VMs in that subnet.
    - You can associate different NSGs to a NIC (or VM, depending on the deployment model) and the subnet that a NIC or VM is bound to. Priority is given based on the direction of traffic.
    - Supports TCP, UDP, and ICMP, and operate at Layer 4 of the OSI model.
    - 5-tuple information (source, source port, destination, destination port, and protocol) to allow or deny the traffic
    - Can use Service tags for simplifying the configuration of your security rules.
    - Application security groups: let you configure network security for resources used by specific apps. You can group VMs logically, no matter what their IP address or subnet assignment.
    - You can use Azure service tags, which represent a group of IP address prefixes from a given Azure service, to permit specific access. More info: https://docs.microsoft.com/en-us/azure/virtual-network/service-tags-overview

- Virtual network service endpoints: for extending your private address space in Azure by providing a direct connection to your Azure services. Basically it creates a route table for the subnet and routes all traffic from a subnet or VNet to the Azure service, for example Azure Storage. Seamlessly it adjusts, for example, the Azure Storage firewall to only allow access from that particular subnet.
    - List of supported Azure Services: https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview
    - PaaS services, such as Azure Storage, are configured to be able to identify traffic coming from your virtual network and allow that, without the need to configure public IP’s on your VNet to allow filtering. Service Endpoints work by enabling a subnet, or subnets, on your virtual network to support Service Endpoints. Once this is done, you can configure your PaaS resource to only accept traffic from those subnets.
        - Service Endpoints cannot be used by traffic originating on-premises, through VPN or Express Route, only for traffic coming from your Azure Virtual Networks.
    - Service Endpoint Policies: Virtual Network (VNet) service endpoint policies allow you to filter egress virtual network traffic to Azure Storage accounts over service endpoint, and allow data exfiltration to only specific Azure Storage accounts. For example, within a VNet you only want to allow one particular subnet to communicate to one particular Azure Service endpoint, all other subnets are not allowed to communicate to the particular Azure Service. Service Endpoint Policies would allow you to create such fine-grained rules.

- Virtual network peering: connect virtual networks
    - Virtual network peering: connects virtual networks in the same Azure region, such as two virtual networks in North Europe.
    - Global virtual network peering: connects virtual networks that are in different Azure regions, such as a virtual network in North Europe and a virtual network in West Europe.
    - Cross-subscription virtual network peering.
    - Virtual network peering is nontransitive.
    - Gateway transit: enable on-premises connectivity without deploying virtual network gateways to all your virtual networks.
    - Avoid overlapping address spaces

- Azure VPN gateways: A VPN gateway is a type of Virtual Network Gateway.
    - Can be used for ExpressRoute failover.
    - VPN gateways can deployed as active/standby or active/active.
    - Require on-premises resources, e.g. VPN device.
    - Can be policy-based (specify statically the IP addresses) or route-based (IPSec tunnels as network interfaces).
    - VPN gateways are deployed in Azure virtual networks and enable the following connectivity:
        - Connect on-premises datacenters to Azure virtual networks through a site-to-site connection.
        - Connect individual devices to Azure virtual networks through a point-to-site connection.
        - Connect Azure virtual networks to other Azure virtual networks through a network-to-network connection.
    - Support zone-redundant configurations in some regions.
    - Requires a GatewaySubnet: called GatewaySubnet

- Azure ExpressRoute: seamlessly extend your on-premises networks into the Microsoft cloud
    - For high-throughput, low-latency connections, and predictable performance
    - Layer 3 connectivity (address-level)
    - Built-in redundancy
    - Connectivity to Microsoft cloud services: Microsoft Office 365, Microsoft Dynamics 365
    - ExpressRoute Global Reach: connect different private datacenters through two ExpressRoute circuits
    - Dynamic routing: Border Gateway Protocol (BGP) is used to exchange routes between on-premises networks and resources running in Azure.
    - ExpressRoute connectivity models:
        - CloudExchange co-location: for co-located at a cloud exchange such as an internet service provider (ISP)
        - Point-to-point Ethernet connection: for example, if you have an on-premises datacenter.
        - Any-to-any connection: For integrating your local wide area network (WAN).
    - Alternatives to ExpressRoute:
        - Site-to-site VPN: VPN device with a public IP address, through an Azure virtual network gateway.
            - Uses an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel
                - IKEv2 VPN is a standards-based IPsec VPN solution that uses outbound UDP ports 500 and 4500 and IP protocol no. 50.
            - Requires your VPN appliance or device to be configured.
        - Point-to-site VPN: from individual computers located on-premises.
            - Uses A VPN client configuration package, which must be generated and installed on every client computer that connects.
            - Uses a PKI certificate, which must be uploaded to Azure.
    - Azure private peering: Private peering is a trusted extension of your core network in Azure with bidirectional connectivity. By using this peering model, you can connect to virtual machines and cloud services directly on their private IP addresses.
    - Microsoft peering: Microsoft peering provides connectivity to all Microsoft online services: Office 365, Dynamics 365, and Azure platform as a service (PaaS).
    - ExpressRoute circuits support a maximum bandwidth of 100 Gbps.

- Azure Load Balancer: used to distribute traffic across multiple virtual machines or applications
    - Hash-based distribution algorithm. By default, a five-tuple hash (source IP, source port, destination IP, destination port, and protocol type) is used to map traffic to available servers. Source IP affinity, also known as session affinity or client IP affinity, for only source IP address to destination IP address. However you can alsouse a three-tuple or two-tuple.
    - Availability sets: An availability set is a logical grouping that you use to isolate virtual machine resources from each other when they're deployed
    - Availability zones: An availability zone offers groups of one or more datacenters that have independent power, cooling, and networking.
    - Can be internal or external (public facing)
    - When you create a load balancer, you must also consider these configuration elements:
        - Front-end IP configuration – A load balancer can include one or more front-end IP addresses. These IP addresses serve as ingress for the traffic.
        - Back-end address pool – IP addresses that are associated with the NIC to which load is distributed.
        - Port Forwarding - Defines how inbound traffic flows through the front-end IP and distributed to the back-end IP utilizing inbound NAT rules.
        - Load balancer rules - Maps a given front-end IP and port combination to a set of back-end IP addresses and port combination. A single load balancer can have multiple load balancing rules. Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.
        - Probes - Monitors the health of VMs. When a probe fails to respond, the load balancer stops sending new connections to the unhealthy VM. The existing connections are not affected, and new connections are sent to healthy VMs.
        - Outbound rules - An outbound rule configures outbound Network Address Translation (NAT) for all virtual machines or instances identified by the backend pool of your Standard Load Balancer to be translated to the frontend.
    - Global versus regional:
        - Global load-balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services.
        - Regional load-balancing services distribute traffic within virtual networks across virtual machines (VMs) or zonal and zone-redundant service endpoints within a region. You can think of them as systems that load balance between VMs, containers, or clusters within a region in a virtual network.
    - Supports Global load-balancing services: uses an external facing endpoint and distributes traffic to regional load balancers, which use external facing endpoints as well. More info: https://docs.microsoft.com/en-us/azure/load-balancer/cross-region-overview
        - Must be public facing.
        - Requires a home region.
        - Client information isn't abstracted away, so underlying applications will, for example, see the client ip-address.

- Azure Traffic Manager: Azure Traffic Manager is a global load balancer that uses DNS records to route traffic to destinations in multiple Azure regions. Because Traffic Manager uses the DNS system to route traffic, it routes any protocol, not just HTTP traffic. However, Traffic Manager can't route or filter traffic based on HTTP properties, such as client country codes or user-agent headers.
    - Is a service for distribution global (public) traffic.
    - Can be used for any traffic.
    - Uses a Traffic Manager instance, which named 'xxxxx.trafficmanager.net'
    - You typically create an alias, DNS CNAME record, which points to the traffic manager instance address.
    - The duration of the cache is determined by the 'time-to-live' (TTL) property of each DNS record. Shorter values result in faster cache expiry and thus more round-trips to the Traffic Manager name servers.
    - Azure endpoints are used for services hosted in Azure. These can be services like Azure App Service, as well as public IP resources that are associated with load balancers or virtual machines.
    - External endpoints are used for IPv4/IPv6 addresses, FQDNs, or for services hosted outside Azure that can either be on-premises or with a different hosting provider.
    - Nested endpoints are used to combine Traffic Manager profiles to create more flexible traffic-routing schemes to support the needs of larger, more complex deployments.
    - Traffic Manager routing methods:
        - Weighted routing
        - Performance routing (latency)
        - Geographic routing
        - Multi-value routing: for multiple healthy endpoints in a single DNS query response
        - Subnet routing: maps the set of user IP address ranges to specific endpoints
        - Priority routing: profile contains a prioritized list of service endpoints

- Application Gateway: routes traffic to a pool of web servers based on the URL of a request
    - Path-based routing: uses paths for routing
    - Multiple site hosting: uses multiple DNS names (CNAMEs)
    - Supports redirection - Redirection can be used to another site, or from HTTP to HTTPS.
    - Supports rewrite HTTP headers - HTTP headers allow the client and server to pass additional information with the request or the response.
    - Supports custom error pages - Application Gateway allows you to create custom error pages instead of displaying default error pages.
    - Can be combined with Service Endpoints. For example, you can think of a scenario in which you want to proxy all traffic from a subnet to a particular service endpoint. This allows network, which use peering, to access the service eindpoint as well.

- Comparing Azure load balancing services: 
    - Front Door (Global & HTTPS) is an application delivery network that provides global load balancing and site acceleration service for web applications. It offers Layer 7 capabilities for your application like SSL offload, path-based routing, fast failover, caching, etc. to improve performance and high-availability of your applications.
    - Traffic Manager (Global & non-HTTPS) is a DNS-based traffic load balancer that enables you to distribute traffic optimally to services across global Azure regions, while providing high availability and responsiveness. Because Traffic Manager is a DNS-based load-balancing service, it load balances only at the domain level. For that reason, it can't fail over as quickly as Front Door, because of common challenges around DNS caching and systems not honoring DNS TTLs.
    - Application Gateway (Regional & HTTPS) provides application delivery controller (ADC) as a service, offering various Layer 7 load-balancing capabilities. Use it to optimize web farm productivity by offloading CPU-intensive SSL termination to the gateway.
    - Azure Load Balancer (Global/Regional & non-HTTPS) is a high-performance, ultra low-latency Layer 4 load-balancing service (inbound and outbound) for all UDP and TCP protocols. It is built to handle millions of requests per second while ensuring your solution is highly available. Azure Load Balancer is zone-redundant, ensuring high availability across Availability Zones.
    - Overview and considerations with different load balancing options: https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/load-balancing-overview

- Azure routing: for controlling traffic flow within your virtual network
    - Virtual network gateway: for sending encrypted traffic between Azure and on-premises over the internet and to send encrypted traffic between Azure networks. A virtual network gateway contains routing tables and gateway services.
    - Virtual network service endpoint: Virtual network endpoints extend your private address space in Azure by providing a direct connection to your Azure resources.
    - Virtual network peering and service chaining: Service chaining lets you override routes by creating user-defined routes between peered networks.
    - Custom routes: create a user-defined route or use Border Gateway Protocol (BGP) to exchange routes between Azure and on-premises networks.
    - User-defined routes: use a user-defined route to override the default system routes so that traffic can be routed through firewalls or NVAs.
    - Border gateway protocol: BGP is used to transfer data and information between different host gateways like on the internet or between autonomous systems.
    - Route selection and priority: If multiple routes share the same address prefix, Azure selects the route based on its type in the following order of priority: 1) User-defined routes 2) BGP routes 3) System routes.
    - Network virtual appliance (NVA): NVAs are virtual machines that control the flow of network traffic by controlling routing. You typically use them to manage traffic flowing from a perimeter-network environment to other networks or subnets.

- Hub and spoke Azure virtual network architecture: A hub and spoke consists of a centralized architecture (a hub) connecting to multiple points (spokes)
    - Integration of separate working environments into a central location for shared services.
    - Traffic routing through the central hub, so workloads can be managed centrally.
    - Required NVA, gateways and complex routing rules.
    - Use NSGs for securing hub and spokes.
    - You use circuits to manage and route traffic. For the standard tier, the limit is currently 10 networks. For premium up to 100 for circuits that are 10-Gbps or bigger.
    - Perimeter network: Configure a perimeter network in its own subnet in the hub virtual network for routing external traffic. Perimeter networks enable secure connectivity between your cloud networks and your on-premises or physical datacenter networks, along with any connectivity to and from the internet. A perimeter network is sometimes called a demilitarized zone or DMZ.
    - Network virtual appliance: Network virtual appliances (NVAs) can provide a secure network boundary by checking all inbound and outbound network traffic.

- Azure Firewall: protects Azure virtual networks and their resources by letting you manage and enforce connectivity policies centrally. 
    - Uses a static, public IP address for virtual network resources, allowing outside firewalls to identify your virtual network traffic.
    - Supports Fully Qualified Domain Names (FQDNs), such as *.domain.com
    - Azure Firewall can be configured during deployment to span multiple Availability Zones for increased availability.
    - Outbound SNAT support: All outbound virtual network traffic IP addresses are translated to the Azure Firewall public IP (Source Network Address Translation). You can identify and allow traffic originating from your virtual network to remote Internet destinations. 
    - Inbound DNAT support: Inbound Internet network traffic to your firewall public IP address is translated (Destination Network Address Translation) and filtered to the private IP addresses on your virtual networks.
    - You can associate multiple public IP addresses (up to 250) with your firewall.
    - Azure Firewall is integrated with Azure Monitor Logs.

- Azure Network Watcher: Monitoring and Diagnostic tools that you can use to monitor your virtual networks and virtual machines (VMs)
    - Topology: generates a graphical display of your Azure virtual network, its resources, its interconnections, and their relationships with each other.
    - Connection Monitor: provides a way to check that connections work between Azure resources.
    - Network Performance Monitor: enables you to track and alert on latency and packet drops over time. It gives you a centralized view of your network.
    - IP flow verify tool: tells you if packets are allowed or denied for a specific virtual machine
    - Next hop tool: determines how a packet gets from a VM to any destination.
    - Effective security rules tool: displays all the effective NSG rules applied to a network interface.
    - Packet capture tool: used to record all of the packets sent to and from a VM.
    - Connection troubleshoot tool: used to troubleshoot or check TCP connectivity between a source and destination VM.
    - VPN troubleshoot tool: used to diagnose problems with virtual network gateway connections.

- Azure DDoS Protection Standard: Azure DDoS Protection Standard provides additional mitigation capabilities over the basic service tier that are tuned specifically to Azure Virtual Network resources. DDoS protection standard is simple to enable and requires no application changes.

- Azure Private Link: Azure Private Link provides private connectivity from a virtual network to Azure platform as a service (PaaS), customer-owned, or Microsoft partner services. It simplifies the network architecture and secures the connection between endpoints in Azure by eliminating data exposure to the public internet.
    - Azure Private Endpoint: Azure Private Endpoint is a network interface that connects you privately and securely to a service powered by Azure Private Link. Private Endpoint uses a private IP address from your VNet, effectively bringing the service into your VNet. The service could be an Azure service such as Azure Storage, Azure Cosmos DB, SQL, etc. or your own Private Link Service. More info: https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview
    - When you create a private endpoint, the DNS CNAME resource record for the storage account is updated to an alias in a subdomain with the prefix privatelink, for example StorageAccountA.privatelink.blob.core.windows.net
    - Azure Private Link service: Azure Private Link service is the reference to your own service that is powered by Azure Private Link. Your service that is running behind Azure Standard Load Balancer can be enabled for Private Link access so that consumers to your service can access it privately from their own VNets. Your customers can create a private endpoint inside their VNet and map it to this service. More info: https://docs.microsoft.com/en-us/azure/private-link/private-link-service-overview
    - Private Link requires you to implement DNS changes (Azure Private Endpoint DNS configuration) and possibly use Azure Private DNS. More info: https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-dns
    - Unlike Service Endpoints, Private Link allows access from resources on your on-premises network through VPN or ExpressRoute, and from peered networks. You can also connect to resources across regions.
    - With Private Link, you are granting access to a specific PaaS resource in your virtual network. That means you can control egress to PaaS resources. For example, if you wanted to, you could use NSG’s to block access to all Azure SQL databases and then use Private Link to grant access only to your specific Azure SQL Server.

### Architect storage infrastructure in Azure

- Azure Storage Accounts: A storage account is a container that groups a set of Azure Storage services together. Only data services from Azure Storage can be included in a storage account (Azure Blobs, Azure Files, Azure Queues, and Azure Tables).
    - Top-level namespaces. DNS is used for namespace, which URIs: http(s)://<account>.<service>.core.windows.net/<partition>/<object>
    - Created within a region. In general you create the storage account within the region that is close to the usage.
    - Core storage services:
        - Azure Blobs: A massively scalable object store for text and binary data. Also includes support for big data analytics through Data Lake Storage Gen2. Ideal for: serving images or documents directly to a browser, storing video and images, backup and restore and data analysis.
            - The Azure Blobs storage service offers three types of blobs: block blobs, append blobs, and page blobs. 
                - Block blobs are optimized for uploading large amounts of data efficiently.
                - Append blobs, ideal for logging, are composed of blocks and is optimized for append operations.
                - Page blobs, ideal for VMs, are a collection of 512-byte pages optimized for random read and write operations.
            - Can be used to host a static website (enables at account level). Populate content in a $web folder.
        - Azure Files: Managed file shares for cloud or on-premises deployments.
        - Azure Queues: A messaging store for reliable messaging between application components. Queue messages can be up to 64 KB in size, and a queue can contain millions of messages. Queues are generally used to store lists of messages to be processed asynchronously.
        - Azure Tables: A NoSQL store for schemaless storage of structured data. Azure Table storage is now part of Azure Cosmos DB.
            - PartitionKey: The PartitionKey property stores string values that identify the partition that an entity belongs to, for example a country or account code. Partitions are integral to the scalability of the table. Entities that have the same PartitionKey value are stored in the same partition.
            - RowKey: The RowKey property stores string values that uniquely identify entities within each partition, for example customer identifier. The PartitionKey and the RowKey together form the primary key for the entity. All entities within a partition are sorted lexically, in ascending order, by this key. The partition key/row key combination must be unique for each entity and cannot exceed 1 KB in length.
            - Timestamp: The Timestamp property provides traceability for an entity. A timestamp is a date/time value that tells you the last time the entity was modified. A timestamp is sometimes referred to as the entity's version. Modifications to timestamps are ignored because the table service maintains the value for this property during all insert and update operations.
        - Azure Disks: Block-level storage volumes for Azure VMs. An Azure managed disk is a virtual hard disk (VHD).
    - Two types of data replication:
        - Intra-stamp replication (stream layer) - Synchronous and keeps data durable within the stamps
        - Inter-stamp replication (partition layer) - Asynchronous replicatioj of data across stamps
    - StorageV2 (general purpose v2): the current offering that supports all storage types and all of the latest features.
    - Storage (general purpose v1): a legacy kind that supports all storage types but may not support all features.
    - Blob storage: a legacy kind that allows only block blobs and append blobs.
    - Azure SQL and Azure Cosmos DB are managed as independent Azure resources and cannot be included in a storage account.
    - Replication: Determines the strategy used to make copies of your data to protect against hardware failure or natural disaster
        - Locally redundant storage (LRS): Locally redundant storage replicates data and stores three copies across fault domains, or racks of hardware, within a single datacenter facility in one region.
        - Zone-redundant storage (ZRS): Zone-redundant storage replicates your data across three availability zones in one region.
        - Geographically redundant storage (GRS): Geographically redundant, or geo-redundant, storage provides multiple levels of replication. Your data is replicated three times within the primary region, and then this set is replicated to a secondary region.
        - Read-access geo-redundant storage (RA-GRS): It is based on the GRS, but it also provides an option to read from the secondary region, regardless of whether Microsoft initiates a failover from the primary to the secondary region.
        - Geo-zone-redundant storage (GZRS): With this replication type, your data is copied across three availability zones in one region. Data is also replicated three times to another secondary region that's paired with it. 
        - Read-access geo-zone-redundant storage (RA-GZRS): Read-access geo-zone-redundant storage (RA-GZRS) uses the same replication method as GZRS but lets you read from the secondary region.
    - Access tier: Controls how quickly you will be able to access the blobs in this storage account.
        - Hot or cold: for frequent or low-frequent used storage.
            - Only the hot and cool access tiers can be set at the account level.
            - Hot tier: The hot access tier has higher storage costs than cool and archive tiers, but the lowest access costs.
            - Cool tier: This tier is intended for data that will remain in the cool tier for at least 30 days. 
        - Archive - Optimized for storing data that is rarely accessed and stored for at least 180 days with flexible latency requirements, on the order of hours.
            - Not directly accessible.
            - The archive access tier can only be set at the blob level.
    - Available tools: Azure Portal, Azure CLI (Command-line interface), Azure PowerShell, Management client libraries
    - You can use Object replication to replicate data to a different storage account. This is useful is you want to apply fine-grained filters. For example, only replicate CSV files within a particular time window.

- Azure Data Lake Storage Gen2: Azure Data Lake Storage is a comprehensive, scalable, and cost-effective data lake solution for big data analytics built into Azure.
    - Hierarchial file system, unlike Azure Blob Storage which has flat namespaces.
    - Hadoop compatible access: A benefit of Data Lake Storage Gen2 is that you can treat the data as if it's stored in a Hadoop Distributed File System. With this feature, you can store the data in one place and access it through compute technologies including Azure Databricks, Azure HDInsight, and Azure Synapse Analytics without moving the data between environments.
    - Security: Data Lake Storage Gen2 supports access control lists (ACLs) and Portable Operating System Interface (POSIX) permissions.
    - Performance: Azure Data Lake Storage organizes the stored data into a hierarchy of directories and subdirectories, much like a file system, for easier navigation. If you want to enable the best performance for analytical workloads in Data Lake Storage Gen2, then on the Advanced tab of the Storage Account creation set the Hierarchical Namespace to Enabled.
    - Data redundancy: Data Lake Storage Gen2 takes advantage of the Azure Blob replication models that provide data redundancy in a single data center with locally redundant storage (LRS), or to a secondary region by using the Geo-redundant storage (GRS) option.

- Azure Storage security features
    - Default rule is to allow all connections from all networks
    - Encryption at rest: all data in Azure is encrypted by Storage Service Encryption (SSE) with a 256-bit Advanced Encryption Standard (AES) cipher, and is FIPS 140-2 compliant.
        - There are two top-level types of encryption: symmetric and asymmetric:
            - Symmetric encryption uses the same key to encrypt and decrypt data.
            - Asymmetric encryption uses a public and private key pair. Asymmetric encryption is used for things like TLS (used in HTTPS), and data syncing.
            - Either key can encrypt, but cannot decrypt its own encrypted data. To decyrpt, you need the paired key.
        - You can configure an encryption scope that enables encryption on container- or blob- level.
    - Encryption in transit: secure data by enabling transport-level security (HTTPS)
        - Azure uses the Transport Layer Security (TLS).
    - For virtual machines (VMs), Azure lets you encrypt virtual hard disks (VHDs) by using Azure Disk Encryption. This encryption uses BitLocker for Windows images, and it uses dm-crypt for Linux.
    - Azure Key Vault stores the keys automatically to help you control and manage the disk-encryption keys and secrets. So even if someone gets access to the VHD image and downloads it, they can't access the data on the VHD.
    - CORS support: Azure Storage supports cross-domain access through cross-origin resource sharing (CORS). CORS uses HTTP headers so that a web application at one domain can access resources from a server at a different domain.
    - Role-based access control: Azure Storage supports Azure Active Directory and role-based access control (RBAC) for both resource management and data operations.
    - Secure access to storage accounts:
        - Azure Active Directory (Azure AD) integration for blob and queue data. 
        - Azure AD authorization over SMB for Azure Files.
        - Authorization with Shared Key.
        - Anonymous access to containers and blobs.
        - Storage account keys (access keys): In Azure Storage accounts, shared keys are called storage account keys. Azure creates two of these keys (primary and secondary) for each storage account you create. The keys give access to everything in the account.
            - Protect shared keys: The storage account has only two keys, and they provide full access to the account. Because these keys are powerful, use them only with trusted in-house applications that you control completely.
        - SAS: For untrusted clients, use a shared access signature (SAS). A SAS is a string that contains a security token that can be attached to a URI. Use a SAS to delegate access to storage objects and specify constraints, such as the permissions and the time range of access.
            - You can use a service-level SAS to allow access to specific resources in a storage account. You'd use this type of SAS, for example, to allow an app to retrieve a list of files in a file system, or to download a file.
            - Use an account-level SAS to allow access to anything that a service-level SAS can allow, plus additional resources and abilities. For example, you can use an account-level SAS to allow the ability to create file systems.
    - Azure Defender for Storage provides an extra layer of security intelligence that detects unusual and potentially harmful attempts to access or exploit storage accounts. This layer of protection allows you to address threats without being a security expert or managing security monitoring systems. It detects anomalies in account activity. It then notifies you of potentially harmful attempts to access your account.
    - Snapshot support: point-in-time view of blobs or files shares that is read-only.
    - Blob versioning support
    - Soft delete, which allows you to undelete files

- Azure File Sync: Azure File Sync is a service that allows you to cache several Azure file shares on an on-premises Windows Server or cloud VM.
    - You can replicate data between different locations, both on-premises and Cloud.
    - Resillience via Previous Versions and VSS (Volume Shadow Copy Service) support.
    - Uses a Azure File Sync agent, which must be installed on every node in the cluster. Each node in the cluster must be registered to work with Azure File Sync.

- Azure NetApp Files: Azure NetApp Files service is an enterprise-class, high-performance, metered file storage service. Azure NetApp Files supports any workload type and is highly available by default. You can select service and performance levels and set up snapshots through the service.

- Azure Storage Explorer: allows you to quickly view all the storage services under your account
    - Uses either an Azure account using Azure AD or shared access signature (SAS) URI.
    - Connects by using a storage account name and key.
    - Can also manage Azure Cosmos DB and Data Lake.
    - Can be downloaded as a stand-alone HTML-based tool: https://azure.microsoft.com/en-us/features/storage-explorer/

- AZCopy: AzCopy is a command-line utility that you can use to copy blobs or files to or from a storage account. This article helps you download AzCopy, connect to your storage account, and then transfer files.
    - Can be downloaded from: https://aka.ms/downloadazcopy
    - Can set concurrency to increase speed
    - Has a sync mode to only replicate changes

- Azure Import/Export: Import/Export for Azure Storage provides fast, secured large data migration to the cloud, saving time, money, and hassle compared to network transfer.
    - You can use and ship your own disks (must be encrypted with Bitlocker)
    - Azure Data Box Disk solution lets you send terabytes of on-premises data to Azure in a quick, inexpensive, and reliable way.

- Azure Files: provides a cloud-based file share (SMB: Server Message Block) for storing and sharing files to apps.
    - AzCopy: Command-line tool that offers the best performance, especially for a low volume of small files.
    - Robocopy: Command-line tool shipped with Windows and Windows Server. AzCopy is written to be Azure aware and performs better.
    - Azure Storage Explorer: Graphical file management utility that runs on Windows, Linux, and macOS.
    - Azure portal: Use the portal to import files and folders.
    - Azure File Sync: Can be used to do the initial data transfer, and then uninstalled after the data is transferred.
    - Azure Data Box: If you have up to 35 TB of data and you need it imported in less than a week.

- Azure disk storage
    - Each disk can take one of three roles in a virtual machine:
        - OS disk. One disk in each virtual machine contains the operating system files. The OS disk has a maximum capacity of 2,048 GB.
        - Data disk. You can add one or more data virtual disks to each virtual machine to store data. Each data disk has a maximum capacity of 32,767 GB.
        - Temporary disk. Each virtual machine contains a single temporary disk, which is used for short-term storage applications such as page files and swap files. 
    - Ephemeral OS disks: An ephemeral OS disk is a virtual disk that saves data on the local virtual machine storage. Ephemeral disks work well when you want to host a stateless workload.
    - Managed disks: A managed disk is a virtual hard disk for which Azure manages all the required physical infrastructure. It uses the Azure Storage account underneath. 
        - Simple scalability, High availability, Integration with availability sets and zones, Support for Azure Backup, Granular access control (RBAC), Support for encryption.
        - Allows multiple VMs (cluster) connecting to the same disk.
    - Unmanaged disks: An unmanaged disk, like a managed disk, is stored as a page blob in an Azure Storage account. The difference is that with unmanaged disks, you create and maintain this storage account manually.
    - Disk types:
        - Ultra SSD: Ultra SSDs provide the highest disk performance available in Azure. They don't support disk snapshots, virtual machine images, scale sets, Azure Disk Encryption, Azure Backup, or Azure Site Recovery. Up to 160,000 IOPS.
        - Premium SSD: Premium SSDs are the next tier down from ultra disks in terms of performance, but they still provide high throughput and IOPS with low latency. They're available in all regions and can be used with virtual machines that are outside of availability zones. Up to 20,000 IOPS.
        - Standard SSD: Standard SSDs in Azure are a cost-effective storage option for virtual machines that need consistent performance at lower speeds. Range of 1 millisecond to 10 milliseconds and up to 6,000 IOPS
        - Standard HDD: Standard HDDs, data is stored on conventional magnetic disk drives with moving spindles. Up to 2,000 IOPS.

### Architect compute infrastructure in Azure

- Azure compute services: Azure compute is an on-demand computing service for running cloud-based applications. It provides computing resources such as disks, processors, memory, networking, and operating systems.
    - Azure Virtual Machines: Virtual machines are software emulations of physical computers. They include a virtual processor, memory, storage, and networking resources.
    - Azure App Service: With Azure App Service, you can quickly build, deploy, and scale enterprise-grade web, mobile, and API apps running on any platform.
        - Web apps: App Service includes full support for hosting web apps by using ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP, or Python. 
        - API apps: Much like hosting a website, you can build REST-based web APIs by using your choice of language and framework. You get full Swagger support and the ability to package and publish your API in Azure Marketplace. 
        - WebJobs: You can use the WebJobs feature to run a program (.exe, Java, PHP, Python, or Node.js) or script (.cmd, .bat, PowerShell, or Bash) in the same context as a web app, API app, or mobile app.
        - Mobile Apps, included as part of Azure App Service, is a backend as a service that provides multiple features to make it easier and quicker to create a mobile application. Mobile Apps is both flexible and scalable, so when your application becomes widely used, you can scale appropriately to handle your customers’ needs.
    - Azure Container Instances: Container Instances are Azure compute resources that you can use to deploy and manage containers. Containers are lightweight, virtualized application environments. 
    - Azure Kubernetes Service: Azure Kubernetes Service is a complete orchestration service for containers with distributed architectures and large volumes of containers. The task of automating, managing, and interacting with a large number of containers is known as orchestration.
    - Azure Functions: Functions are ideal when you're concerned only about the code running your service and not the underlying platform or infrastructure.
        - Abstraction of servers, Event-driven scale, Micro-billing.
    - Windows Virtual Desktop: Windows Virtual Desktop on Azure is a desktop and application virtualization service that runs on the cloud. It enables your users to use a cloud-hosted version of Windows from any location.
        - Simplified management, Performance management (Host pools are collections of VMs with the same configuration assigned to multiple users), Multi-session Windows 10 deployment

- Azure provisioning tools: a way to automate the provisioning and management of compute resources
    - Custom script: The custom script extension downloads and runs scripts on Azure virtual machines. This tool is useful for post-deployment configuration, software installation, or any other configuration or management task.
        - Ease of setup. The custom script extension is built into the Azure portal, so setup is easy.
        - Management. The management of custom scripts can get tricky as your infrastructure grows and you accumulate different custom scripts for different resources.
        - Interoperability. The custom script extension can be added into an Azure Resource Manager template. You can also deploy it through Azure PowerShell or the Azure CLI.
        - Configuration language. You can write scripts by using many types of commands. You can use PowerShell and Bash.
        - Limitations and drawbacks. Custom scripts aren't suitable if your script needs more than one and a half hours to apply your configuration. Avoid using custom scripts for any configuration that needs reboots.    
    - Azure Desired State Configuration extensions: Desired State Configuration (DSC) extensions make it possible for you to deal with the configurations on your infrastructure that might need more complex installation procedures, such as reboots. DSC helps you define a state for your machines instead of writing detailed manual instructions on how to achieve that state for each machine.
        - Ease of setup. Desired State Configurations (DSCs) are easy to read, update, and store. Configurations define what state you want to achieve. The author doesn't need to know how that state is reached.
        - Management. DSC democratizes configuration management across servers.
        - Interoperability. DSCs are used with Azure Automation State Configuration. They can be configured through the Azure portal, Azure - PowerShell, or Azure Resource Manager templates.
        - Configuration language. Use PowerShell to configure DSC.
        - Limitations and drawbacks. You can only use PowerShell to define configurations. If you use DSC without Azure Automation State Configuration, you have to take care of your own orchestration and management.
    - Azure Automation State Configuration: Azure automation state configuration is the service you use to make sure that your DSC configurations are managed properly and deployed across your nodes (virtual machines). 
        - Ease of setup. Automation State Configuration isn't difficult to set up, but it requires the user to be familiar with the Azure portal.
        - Management. The service manages all of the virtual machines for you automatically. Each virtual machine can send you detailed reports about its state, which you can use to draw insights from this data. Automation State Configuration also helps you to manage your DSC configurations more easily.
        - Interoperability. Automation State Configuration requires DSC configurations. It works with your Azure virtual machines automatically, and any virtual machines that you have on-premises or on another cloud provider.
        - Configuration language. Use PowerShell.
        - Limitations and drawbacks. You can only use PowerShell to define configurations.
    - Azure Resource Manager templates: Azure Resource Manager templates are JSON files that you can use to define the Azure resources you want to provision in Azure through object notation.
        - Ease of setup. You can create Resource Manager templates easily. You have many templates available from the GitHub community, which you can use or build upon. Alternatively, you can create your own templates from the Azure portal.
        - ARM deplotments are declarative. You specify what you want to deploy. It validates, and if resources don't exist it will create them for you. You don't have to validate yourself. Thus you can safely rerun this without the risk that resources are created multiple times.
        - Management. Managing Resource Manager templates is straightforward because you manage JavaScript Object Notation (JSON) files.
        - Interoperability. You can use other tools to provision Resource Manager templates, such as the Azure CLI, the Azure portal, PowerShell, and Terraform.
        - Configuration language. Use JSON.
        - Limitations and drawbacks. JSON has a strict syntax and grammar, and mistakes can easily render a template invalid. The requirement to know all of the resource providers in Azure and their options can be onerous.
        - Bicep: Bicep is a language for declaratively deploying Azure resources. You can use Bicep instead of JSON for developing your Azure Resource Manager templates (ARM templates). Bicep simplifies the authoring experience by providing concise syntax, better support for code reuse, and improved type safety. More info: https://github.com/Azure/bicep
        - Can be combined with GitHub Action for automatic deployments:
            - Azure CLI: https://github.com/Azure/cli
            - Use GitHub Actions to connect to Azure: https://docs.microsoft.com/en-us/azure/developer/github/connect-from-azure

- Azure Resource Manager: Azure Resource Manager is the interface for managing and organizing cloud resources. Think of Resource Manager as a way to deploy cloud resources.
    - A Resource Manager template precisely defines all the Resource Manager resources in a deployment. You can deploy a Resource Manager template into a resource group as a single operation.
    - Benefits to consider: Templates improve consistency, Templates help express complex deployments, Templates reduce manual, error-prone tasks, Templates are code, Templates promote reuse, Templates are linkable
    - Parameters: This is where you specify which values are configurable when the template runs.
    - Variables: This is where you define values that are used throughout the template. Variables can help make your templates easier to maintain.
    - Functions: This is where you define procedures that you don't want to repeat throughout the template. Like variables, functions can help make your templates easier to maintain.
    - Resources: This section is where you define the Azure resources that make up your deployment. All template resources provide a dependsOn property. This property helps Resource Manager determine the correct order to apply resources.
    - Outputs: This is where you define any information you'd like to receive when the template runs.
    - Azure Quickstart templates: Azure Quickstart templates are Resource Manager templates that are provided by the Azure community. Quickstart templates are available on GitHub: https://github.com/Azure/azure-quickstart-templates
    - Custom Script Extension: The Custom Script Extension is an easy way to download and run scripts on your Azure VMs. It's just one of the many ways you can configure a VM once it's up and running.

- Azure Virtual Machines: Virtual machines are software emulations of physical computers. They include a virtual processor, memory, storage, and networking resources.
    - Comes in different sizes: https://docs.microsoft.com/en-us/azure/virtual-machines/sizes
        - Some VM types have burst capabilities.
    - Virtual machine scale sets are an Azure compute resource that you can use to deploy and manage a set of identical VMs. With all VMs configured the same, virtual machine scale sets are designed to support true autoscale.
        - A scale set uses a load balancer to distribute requests across the VM instances. It uses a health probe to determine the availability of each instance. The health probe pings the instance.
        - Horizontal scaling is the process of adding or removing several VMs in a scale set.
        - Vertical scaling is the process of adding resources such as memory, CPU power, or disk space to VMs.
        - Scheduled scaling: You can proactively schedule the scale set to deploy one or N number of additional instances to accommodate a spike in traffic and then scale back down when the spike ends.
        - Autoscaling: If the workload is variable and can't always be scheduled, you can use metric-based threshold scaling. Autoscaling horizontally scales out based on node usage. It then scales back in when the resources return to a baseline.
    - Azure Batch enables large-scale parallel and high-performance computing (HPC) batch jobs with the ability to scale to tens, hundreds, or thousands of VMs.
    - Examples of when to use VMs: During testing and development, When running (traditional) applications in the cloud, When extending your datacenter to the cloud, During disaster recovery.
    - Generalized image: Image that can be used to quickly setup multiple virtual machines from the same generic state.
    - Specialized virtual image: A specialized virtual image is a copy of a live virtual machine after it has reached a specific state.
    - Availability Set: Availability Sets ensure that the Azure virtual machines are deployed across multiple isolated hardware nodes in a cluster. By deploying your vms across multiple hardware nodes Azure ensures that if hardware or software failure happens within Azure, only a sub-set of your virtual machines are impacted and your overall solution is safe and in working condition. Availability set provides redundancy for your virtual machines. Availability set spreads your virtual machines across multiple fault domains and update domains.
    - Fault Domain: Fault domains define the group of virtual machines that share a common power source and network switch. Each and every fault domain contains some racks and each rack contains virtual machine. Each of these Fault domain shares a power supply and a network switch. If there is a failure in the fault domain then all the resources in the fault domain become unavailable.
    - Update Domains: Virtual machines get update domains automatically once they are put inside availability set. All virtual machines within that update domain will reboot together. Update domains are used for patching of the virtual machines. Only one update domain would be updated at the time.
    - Azure Hybrid Benefit: Azure Hybrid Benefit is a licensing benefit that helps you to significantly reduce the costs of running your workloads in the cloud. It works by letting you use your on-premises Software Assurance-enabled Windows Server and SQL Server licenses on Azure.
    - Azure Reservations: Azure Reservations help you save money by committing to one-year or three-year plans for multiple products. Committing allows you to get a discount on the resources you use. Reservations can significantly reduce your resource costs by up to 72% from pay-as-you-go prices.
    - Proximity placement groups: A proximity placement group is a logical grouping used to make sure that Azure compute resources are physically located close to each other. Proximity placement groups are useful for workloads where low latency is a requirement.
    - Supports Managed Identity.
    - Isolated Virtual Machines: Azure Compute offers virtual machine sizes that are Isolated to a specific hardware type and dedicated to a single customer. The Isolated sizes live and operate on specific hardware generation and will be deprecated when the hardware generation is retired.
    - Azure Dedicated Host: Azure Dedicated Host provides physical servers that host one or more Azure virtual machines. Your server is dedicated to your organization and workloads—capacity isn’t shared with other customers. This host-level isolation helps address compliance requirements.
    - Bare-metal support: BareMetal Infrastructure is intended for mission critical workloads that require certification to run your enterprise applications.
    - VMWare support: Azure VMware Solution provides you with private clouds that contain vSphere clusters, built from dedicated bare-metal Azure infrastructure.

- Microsoft Power Automate: Microsoft Power Automate is a service that you can use to create workflows even when you have no development or IT Pro experience. You can create workflows that integrate and orchestrate many different components by using the website or the Microsoft Power Automate mobile app.
    - Intended users: Office workers and business analysts
    - Intended scenarios: Self-service workflow creation
    - Design tools: GUI only. Browser and mobile app
    - Application Lifecycle Management: Power Automate includes testing and production environments

- Microsoft Power Apps: Power Apps provides a low-code approach to rapidly build apps for any device, while seamlessly working with your Azure-based services through a rich professional developer extensibility model.
    - Power Apps is a suite of apps, services, connectors and data platform that provides a rapid application development environment to build custom apps for your business needs.
    - To create an app, you start with make.powerapps.com.
        - Power Apps Studio is the app designer used for building canvas apps. The app designer makes creating apps feel more like building a slide deck in Microsoft PowerPoint. More information: Generate an app from data
        - App designer for model-driven apps lets you define the sitemap and add components to build a model-driven app. More information: Design model-driven apps using app designer
        - Power Apps portals Studio is a WYSIWYG design tool to add and configure webpages, components, forms, and lists. More information: Power Apps portals Studio anatomy

- Azure Logic Apps: Logic Apps is a service within Azure that you can use to automate, orchestrate, and integrate disparate components of a distributed application. By using the design-first approach in Logic Apps, you can draw out complex workflows that model complex business processes.
    - Intended users: Developers and IT pros
    - Intended scenarios: Advanced integration projects
    - Design tools: Browser and Visual Studio designer. Code editing is possible
    - Application Lifecycle Management: Logic Apps source code can be included in Azure DevOps and source code management systems.
    - Integration Service Environment available for dedicated and isolated environment
    - Initiated via triggers (such as events)
    - There are many connectors and templates to get started

- WebJobs and the WebJobs SDK: The Azure App Service is a cloud-based hosting service for web applications, mobile back-ends, and RESTful APIs. These applications often need to perform some kind of background task.
    - Continuous. These WebJobs run in a continuous loop. For example, you could use a continuous WebJob to check a shared folder for a new photo.
    - Triggered. These WebJobs run when you manually start them or on a schedule.

- Azure Functions: An Azure Function is a simple way for you to run small pieces of code in the cloud, without having to worry about the infrastructure required to host that code.
    - Two implementations of serverless compute:
        - Azure Functions: Functions can execute code in almost any modern language.
        - Azure Logic Apps: Logic apps (stateful) are designed in a web-based designer and can execute logic triggered by Azure services without writing any code.
    - HTTPTrigger. Use this template when you want the code to execute in response to a request sent through the HTTP protocol.
    - TimerTrigger. Use this template when you want the code to execute according to a schedule.
    - BlobTrigger. Use this template when you want the code to execute when a new blob is added to an Azure Storage account.
    - CosmosDBTrigger. Use this template when you want the code to execute in response to new or updated documents in a NoSQL database.
    - Azure Function can run on a App Service consumption plan, so you only pay when the function runs.

- HPC: high-performance computing
    - Azure Batch: Azure Batch is a service for working with large-scale parallel and computationally intensive tasks on Azure.
        - Batch is ideally suited to heavy workloads, such as financial risk modeling, 3D rendering, media transcoding, and genetic sequence analysis. Batch is well-suited to highly parallel workloads, which are sometimes called embarrassingly parallel workloads. 
        - Works with Jobs (configurable settings), Tasks (real unit of work) and Pools (VMs, which are often called nodes)
    - Azure VM HPC instances: Azure H-series VMs are a family of the most powerful and fastest CPU-based VMs on Azure. These VMs are optimized for applications that require high CPU frequencies or large amounts of memory per core.
    - Microsoft HPC Pack: HPC Pack offers a series of installers for Windows that allows you to configure your own control and management plane, and highly flexible deployments of on-premises and cloud nodes.
        - Common HPC use cases: Finite element analysis, 3D model rendering, DNA analysis, Computer-aided design

### Architect infrastructure operations in Azure

- Resource group: Resource groups are a fundamental element of the Azure platform. A resource group is a logical container for resources deployed on Azure.
    - Logical grouping: Resource groups exist to help manage and organize your Azure resources.
    - Cannot be nested.
    - Life cycle: If you delete a resource group, all resources contained within are also deleted. 
    - Authorization: Resource groups are also a scope for applying role-based access control (RBAC) permissions
    - Consistent naming convention: You can start with using an understandable naming convention, such as vm-rg, db-rg, prod-rg, dev-rg, etc.
    - Organizing for billing: Placing resources in the same resource group is a way to group them for usage in billing reports.

- Tags: Tags are name/value pairs of text data that you can apply to resources and resource groups.
    - Not all resources support tags.
    - Tags are not propagated to resources within the resource group. However this can be enabled with an additional flag.
    - Tags are very useful for billing and cost management.
    - Tags can be enforced through policies.
    - Tags are key-value pairs. You can use JSON as values.
    - Azure provides best practises for naming and tagging: https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging

- Azure Policy: Azure Policy is a service you can use to create, assign, and manage policies. These policies apply and enforce rules that your resources need to follow. For example, enforcing specific types of VMs, enforcing resources to be deployed within a specific region, ensuring tags are set, requiring managed disks, requiring diagnostics to be enabled, GEO-replication on production workloads, and so on.
    - Azure Policy focuses on resource properties during deployment and for already-existing resources. Azure Policy controls properties such as the types or locations of resources. Unlike RBAC, Azure Policy is a default-allow-and-explicit-deny system.
    - Azure policy is really three components: policy definition, assignment and parameters:
        - Policy definition: Policy definition is the conditions which you want controlled. There are built in definitions such as controlling what type of resources can be deployed to enforcing the use of tags on all resources.
        - Policy assignment: Policy assignment is the scope of what the policy definition can take effect around. Scope of assignment can be assigned to a individual resource, resource group, or management group. Policy assignments are inherited by all child resources.
        - Policy parameters: Policy parameters help simplify your policy management by reducing the number of policy definitions you must create. Parameters would be used to define which type of VM SKUs to deploy or defining a specific location.
    - RBAC focuses on user actions at different scopes. RBAC provides fine-grained access management for Azure resources, enabling you to grant users the specific rights they need to perform their jobs. RBAC uses an allow model for access. When you are assigned to a role, RBAC allows you to perform specific actions, such as read, write, or delete. RBAC is basically about the 'who'.
        - When you apply RBAC you also set the scope, the set of resources that access applies to. In Azure, you can specify a scope at four levels: management group, subscription, resource group, and resource. Scopes are structured in a parent-child relationship. Each level of hierarchy makes the scope more specific. You can assign roles at any of these levels of scope. The level you select determines how widely the role is applied. Lower levels inherit role permissions from higher levels. More info: https://docs.microsoft.com/en-us/azure/role-based-access-control/scope-overview
    - Policies help you manage and prevent IT issues with policy definitions that enforce rules and effects for your resources. Policies are basically about the 'what'.
    - Resource locks: Resource locks are a setting that can be applied to any resource to block modification or deletion. Resource locks can set to either Delete or Read-only.
    - RBAC rules and policies can be set on both subscriptions, management groups, resource groups and individual resources. Each inherit their RBAC rules and policies from their parent(s).
    - An Azure initiative is a collection of Azure policy definitions that are grouped together towards a specific goal or purpose in mind. Azure initiatives simplify management of your policies by grouping a set of policies together as one single item.

- Azure Blueprint: Is a service that enables you to deploy a collection of Azure resources adhering to specific standards.
    - You can bring together the following artifacts: resource groups, RBAC, ARM JSON, policies and custom scripts.

- Azure Resource Graph: Azure Resource Graph is a service in Azure that is designed to extend Azure Resource Management by providing efficient and performant resource exploration with the ability to query at scale across a given set of subscriptions so that you can effectively govern your environment.
    - Ability to query resources with complex filtering, grouping, and sorting by resource properties. Ability to iteratively explore resources based on governance requirements. Ability to assess the impact of applying policies in a vast cloud environment. Ability to detail changes made to resource properties (preview).
    - Azure Resource Graph Explorer, part of Azure portal, enables running Resource Graph queries directly in Azure portal.

- Cloud Adoption Framework: The Cloud Adoption Framework consists of tools, documentation, and proven practices. 

- Azure Monitor: Azure Monitor is a service for collecting, analyzing, and acting on telemetry from your cloud and on-premises environments.
    - Full stack monitoring in Azure: Full stack monitoring is a complete approach to the monitoring, triage, and diagnosis of application, infrastructure, and security issues that includes telemetry collection, tracking key performance indicators and the capability to isolate problems and perform root cause analysis.
    - Uses Log Analytics as a backend. Remember: each service provides the options to store monitoring data in either storage accounts, EventHubs or Log Analytics, or a combination of these.
    - Uses either custom made solutions or workbooks for showing comprehensive overviews. Only the workbooks can be modified.
    - Azure Monitor collects two types of data: metrics and logs:
        - Metrics are numerical values that describe some aspect of a system at a point in time
        - Logs contain time-stamped information about changes made to resources. The type of information recorded varies by log source.
        - Distributed traces: Traces are series of related events that follow a user request through a distributed system. They can be used to determine behavior of application code and the performance of different transactions. 
    - Azure Monitor starts with collecting telemetry, this data includes application layer data and infrastructure performance data from VM guest operating systems and containers.
    - Azure Monitor Application Insights: For analyzing and addressing issues such as exceptions, failures, and availability problems. For Instrumenting your web pages with Application Insights collects usage information to augment the server-side monitoring capabilities. For availability tests to continuously monitor your application from different geographic locations.
    - Azure Monitor Insights: For getting additional insights in health and performance.
    - Composition of an alert rule:
        - RESOURCE: The target resource to be used for the alert rule.
        - CONDITION: The signal type to be used to assess the rule. The alert logic applied to the data that's supplied via the signal type.
        - ACTION: The action, like sending an email, sending an SMS message, or using a webhook. An action group, which typically contains a unique set of recipients for the action.
        - ACTION DETAILS: An alert name and an alert description that should specify the alert's purpose. The severity of the alert if the criteria or logic test evaluates true. The five severity levels are: Critical (0), Error (1), Warning (2), Informational (3), Verbose (4)
    - The look-back period defines how many previous periods need to be evaluated.
    - The number of violations expresses how many times the logic condition has to deviate from the expected behavior before the alert rule fires a notification.
    - Azure Monitor supports the creation of metric alerts that, like dimensions, monitor multiple resources. Scaling is currently limited to Azure virtual machines.
    - Log alerts use log data to assess the rule logic and, if necessary, trigger an alert. This data can come from any Azure resource: server logs, application server logs, or application logs.
    - Activity log alerts are designed to work with Azure resources. Typically, you create this type of log to receive notifications when specific changes occur on a resource within your Azure subscription.
    - Smart groups are an automatic feature of Azure Monitor. By using machine learning algorithms, Azure Monitor joins alerts based on repeat occurrence or similarity. Smart groups enable you to address a group of alerts instead of each alert individually. The states are: New, Acknowledged, Closed
    - Analyzing logs by using Kusto: To retrieve, consolidate, and analyze data, you specify a query to run in Azure Monitor logs. You write a log query with the Kusto query language, which is also used by Azure Data Explorer.

- Azure Security Center: Azure Security Center is a service that manages the security of your infrastructure from a centralized location. Use Security Center to monitor the security of your workloads, whether they're on-premises or in the cloud.
    - Security Center is natively integrated with other Azure services, such as PaaS services like Azure SQL Database. For IaaS services, enable automatic provisioning in Security Center.
    - Azure Sentinel and Azure Security Center use Azure Monitor Logs (Log Analytics workspace) as their underlying logging data platform.
    - Just-in-time (JIT) virtual machine access: JIT is a feature that blocks persistent access to virtual machines.
    - Uses Azure Defender, as an optional service, for advanced threat protection for virtual machines, SQL databases, containers, web applications, and so on.

- Azure Sentinel: You use Azure Sentinel to collect data on the devices, users, infrastructure, and applications across your enterprise. Built-in threat intelligence for detection and investigation can help reduce false positives. Use Sentinel to proactively hunt for threats and anomalies, and respond by using orchestration and automation.
    - Use playbooks to automate your response to alerts in Sentinel. You configure playbooks by using Azure Logic Apps. Templates can be found here: https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks
    - Uses workbooks to give a comprehensive overview of certain security information. Workbooks look similar to PowerBI reports.
    - You fist create a workspace, and then add that workspace to Azure Sentinel.
    - You can customize with Kusto Query Language your signals.

- Managed Identity: Managed identities eliminate the need for developers to manage credentials. Managed identities provide an identity for applications to use when connecting to resources that support Azure Active Directory (Azure AD) authentication. Applications may use the managed identity to obtain Azure AD tokens.
    - Services that support managed identities for Azure resources: https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/services-support-managed-identities
    - Managed Identities are in essence 100% identical in functionality and use case than Service Principals. In fact, they are actually Service Principals. What makes them different though, is: – They are always linked to an Azure Resource, not to an application or 3rd party connector – They are automatically created for you, including the credentials; big benefit here is that no one knows the credentials.
    - There are two types of managed identities:
        - System-assigned: Some Azure services allow you to enable a managed identity directly on a service instance. When you enable a system-assigned managed identity an identity is created in Azure AD that is tied to the lifecycle of that service instance. So when the resource is deleted, Azure automatically deletes the identity for you. By design, only that Azure resource can use this identity to request tokens from Azure AD. Resources that support system assigned managed identities allow you to: 
            - Enable or disable managed identities at the resource level.
            - Use RBAC roles to grant permissions.
            - View create, read, update, delete (CRUD) operations in Azure Activity logs.
            - View sign-in activity in Azure AD sign-in logs.
        - User-assigned: You may also create a managed identity as a standalone Azure resource. You can create a user-assigned managed identity and assign it to one or more instances of an Azure service. In the case of user-assigned managed identities, the identity is managed separately from the resources that use it. If you choose a user assigned managed identity instead:
            - You can create, read, update, delete the identities.
            - You can use RBAC role assignments to grant permissions.
            - User assigned managed identities can be used on more than one resource.
            - CRUD operations are available for review in Azure Activity logs.
            - View sign-in activity in Azure AD sign-in logs.
    - For many managed services it works natively. For other type of services there is sample code to make a call and get the identity.
    - A Service Principal, which is also managed in Azure AD as an enterprise application, is an application or 3rd party connector whose tokens can be used to authenticate and grant access to specific Azure resources from a user-app, service or automation tool, when an organization is using Azure Active Directory. More info: https://devblogs.microsoft.com/devops/demystifying-service-principals-managed-identities/
        - A Service Principal could be looked at as similar to a service account-alike in a more traditional on-premises application or service scenario. 
        - The Service Principals’ access can be restricted by assigning Azure RBAC roles so that they can access the specific set of resources only. There is one major exception to this RBAC rule, and that is Azure Key Vault, which can be extended by using Key Vault Access Policies to define permissions, instead of Azure RBAC roles.

- Azure Key Vault: Azure Key Vault is a cloud service for securely storing and accessing secrets. A secret is anything that you want to tightly control access to, such as API keys, passwords, certificates, or cryptographic keys.
    - Vaults: You use Azure Key Vault to create multiple secure containers, called vaults. Vaults help reduce the chances of accidental loss of security information by centralizing application secrets storage. Organizations will have several key vaults. Each key vault is a collection of cryptographic keys and cryptographically protected data (call them “secrets”) managed by one or more responsible individuals within your organization. These key vaults represent the logical groups of keys and secrets for your organization; those that you want to manage together. They are like folders in the file system.
    - Keys: Keys are the central actor in the Azure Key Vault service. A given key in a key vault is a cryptographic asset destined for a particular use such as the asymmetric master key of Microsoft Azure RMS, or the asymmetric keys used for SQL Server TDE (Transparent Data Encryption), CLE (Column Level Encryption) and Encrypted backup.
    - Supports Managed Identify
    - Key Vault service supports two types of containers: 
        - Vaults: Vaults support storing software and HSM-backed keys, secrets, and certificates. 
        - Managed hardware security module(HSM) pools: Managed HSM pools only support HSM-backed keys.
    - Useful for situations where you cannot you managed identities.
    - Access policies (generic) or RBAC access model (fine-grained).
        - A Key Vault access policy determines whether a given security principal, namely a user, application or user group, can perform different operations on Key Vault secrets, keys, and certificates.
    - Secrets: Secrets are small (less than 10K) data blobs protected by a HSM-generated key created with the Key Vault. Secrets exist to simplify the process of persisting sensitive settings that almost every application has: storage account keys, .PFX files, SQL connection strings, data encryption keys, etc.

### Architect a data platform in Azure

- Azure Cosmos DB: Azure Cosmos DB is a globally distributed, multi-model database service. You can elastically and independently scale throughput and storage across any number of Azure regions worldwide.
    - Azure Cosmos DB provides five APIs to suit the needs of your application: SQL (relational database), Gremlin (graph database), MongoDB (document database), Azure Table, and Cassandra, each of which currently requires a separate account. SQL API is the preferred data model if you are creating a new application.
    - Request unit basics: A single request unit, one RU, is equal to the approximate cost of performing a single GET request on a 1-KB document using a document's ID. Performing a GET by using a document's ID is an efficient means for retrieving a document, and thus the cost is small. Creating, replacing, or deleting the same item requires additional processing by the service, and therefore requires more request units.
        - Azure Cosmos DB ensures that the number of RUs for a given database operation over a given dataset is deterministic.
        - The size of the document, Item property count, and Indexing policy are considered when provisioning request units.
        - Once you set the number of request units, it's impossible to modify this number.
    - A partition key is the value by which Azure organizes your data into logical divisions. It should aim to evenly distribute operations across the database to avoid hot partitions. You can set the partition key only when the container is created.
    - Multi-master support is an option that can be enabled on new Azure Cosmos DB accounts. Once the account is replicated in multiple regions, each region is a master region that equally participates in a write-anywhere model, also known as an active-active pattern.
    - There are three conflict resolution modes offered by Azure Cosmos DB.
        - Last-Writer-Wins (LWW), in which conflicts are resolved based on the value of a user-defined integer property in the document. By default _ts is used to determine the last written document. Last-Writer-Wins is the default conflict handling mechanism.
        - Custom - User-defined function, in which you can fully control conflict resolution by registering a User-defined function to the collection. A User-defined function is a special type of stored procedure with a specific signature. If the User-defined function fails or does not exist, Azure Cosmos DB will add all conflicts into the read-only conflicts feed they can be processed asynchronously.
        - Custom - Async, in which Azure Cosmos DB excludes all conflicts from being committed and registers them in the read-only conflicts feed for deferred resolution by the user’s application. The application can perform conflict resolution asynchronously and use any logic or refer to any external source, application, or service to resolve the conflict.
    - Consistency levels:
        - Strong: Linearizability. Reads are guaranteed to return the most recent version of an item.
        - Bounded Staleness: Consistent Prefix. Reads lag behind writes by at most k prefixes or t interval.
        - Session: Consistent Prefix. Monotonic reads, monotonic writes, read-your-writes, write-follows-reads. Session is the best consistency setting for user data that contains shopping basket information. Session consistency will ensure that every item the user put in their basket is displayed when they review their basket.
        - Consistent Prefix: Updates returned are some prefix of all the updates, with no gaps.
        - Eventual: Out of order reads. The cost of a read operation with eventual consistency consumes the least number of request units per seconds.
        - About 73% of Azure Cosmos DB tenants use session consistency and 20% prefer bounded staleness. Approximately 3% of Azure Cosmos DB customers experiment with various consistency levels initially before settling on a specific consistency choice for their application. Only 2% of Azure Cosmos DB tenants override consistency levels on a per request basis.
    - Supports stored procedures and user-defined functions
    - Azure Synapse Link for Azure Cosmos DB is a cloud-native hybrid transactional and analytical processing (HTAP) capability that enables you to run near real-time analytics over operational data in Azure Cosmos DB. Azure Synapse Link creates a tight seamless integration between Azure Cosmos DB and Azure Synapse Analytics.
    - Azure Cosmos DB analytical store is a fully isolated column store for enabling large-scale analytics against operational data in your Azure Cosmos DB, without any impact to your transactional workloads. Azure Cosmos DB transactional store is schema-agnostic, and it allows you to iterate on your transactional applications without having to deal with schema or index management. In contrast to this, Azure Cosmos DB analytical store is schematized to optimize for analytical query performance.

- Azure SQL Database: Azure SQL Database is a relational database based on the latest stable version of the Microsoft SQL Server database engine. SQL Database is a high-performance, reliable, fully managed, and secure database.
    - SQL Server on Virtual Machines: SQL Server on Azure Virtual Machines (VMs) is an IaaS offer and allows you to run SQL Server inside a virtual machine in the cloud. This option is most typical for migrating classic workloads from on-premises. In this deployment option you have access to the underlying virtual machine.
        - Up to 256 TB
        - Allows access to VM OS
    - Azure SQL Managed Instance: Azure SQL Managed Instance is a scalable cloud data service that provides the broadest SQL Server database engine compatibility with all the benefits of a fully managed platform as a service.
        - Up to 8 TB.
        - You can migrate or choose an existing license.
        - 100% compatible with on-premises SQL Server (SQL Agent support, DMV extensions, native backup and restore, and so on.)
        - You don't have access to underlying Virtual Machines.
    - Azure SQL Database services: Azure SQL Database is an intelligent, scalable, relational database service built for the cloud.
        - Single databases: The single database resource type creates a database in Azure SQL Database with its own set of resources and is managed via a server. With a single database, each database is isolated and portable.
            - There are two deployment options: provisioned or serverless
                - SQL database elastic pools are a cost-effective service that can manage and scale multiple Azure SQL databases that have varying and unpredictable resource requirements.
                    - You can add multiple SQL elastic pools to a single Azure SQL server.
                    - SQL elastic pools are ideal when you have several SQL databases that have a low average utilization, but have infrequent, high utilization spikes.
                    - At a minimum, it is recommended to add at least two S3 databases or fifteen S0 databases to a single pool for it to have potential cost savings.
                    - Depending on the performance tier, you can add up to 100 or 500 databases to a single pool.
                    - Each has its own service tier within the DTU-based purchasing model or vCore-based purchasing model and a guaranteed compute size.
                - Single databases in Azure SQL Database support manual dynamic scalability, but not autoscale. You can change DTU service tiers or vCore characteristics at any time with minimal downtime to your application (generally averaging under four seconds). With a single database, you can use either DTU or vCore models to define maximum amount of resources that will be assigned to each database.
            - Azure SQL Database serverless: Serverless is a compute tier for single databases in Azure SQL Database that automatically scales compute based on workload demand and bills for the amount of compute used per second.
                - Requires minimum and maximum number of vCores to be set.
            - A single database can be moved into or out of an elastic pool for resource sharing. 
        - SQL Hyperscale: A Hyperscale database is a database in SQL Database in the Hyperscale service tier that is backed by the Hyperscale scale-out storage technology. 
            - A Hyperscale database supports up to 100 TB of data and provides high throughput and performance, as well as rapid scaling to adapt to the workload requirements.
            - Single database that uses multiple read stores underneath.
            - You cannot revert back to a different service tier after you moved your workload into a SQL Hyperscale instance.
            - Doesn't support GEO-replica.
        - General Purpose or Business Critical:
            - General Purpose offers budget oriented balanced compute and storage options.
            - Business Critical: OLTP applications with high transaction rate and low IO latency. Offers highest resilience to failures and fast failovers using multiple synchronously updated replicas.
                - Always-on availability group. One instance supports reads and writes, the other ones are in read-mode.
        - SQL Server Pricing models:
            - DTU-based pricing model: A database transaction unit (DTU) is a unit of measurement for the performance of a service tier in Azure and is based on a bundled measure of compute, storage, and IO resources. Compute sizes are expressed in terms of Database Transaction Units (DTUs) for single databases or elastic Database Transaction Units (eDTUs) for elastic pools.
                - Autoscaling support
                - Allows for more complex configurations
                - Requires you to specify the resources for the required workload.
            - vCore-based pricing model: A virtual core (vCore) represents the logical CPU offered with an option to choose between generations of hardware and physical characteristics of hardware (for example, number of cores, memory, storage size).
                - Combines storage, compute and IO
                - Less granular controls, Simple configuration
    - Data Migration Assistant is a client-side tool that you can install on a Windows-compatible workstation or server.
    - Azure Database Migration Service is a fully-managed Azure service that provides automated, seamless data migrations from multiple sources into the Azure data platforms.
        - There are two options for doing a migration: offline and online (migration with minimal downtime).

- Azure database for MySQL: Azure Database for MySQL is a relational database service in the cloud, and it's based on the MySQL Community Edition database engine, versions 5.6, 5.7, and 8.0.

- Azure Database for PostgreSQL: Azure Database for PostgreSQL is a relational database service in the cloud. The server software is based on the community version of the open-source PostgreSQL database engine. Your familiarity with tools and expertise with PostgreSQL is applicable when you're using Azure Database for PostgreSQL.
    - The Single Server deployment option offers three pricing tiers: Basic, General Purpose, and Memory Optimized.
    - The Hyperscale (Citus) option horizontally scales queries across multiple machines by using sharding. Its query engine parallelizes incoming SQL queries across these servers for faster responses on large datasets.

- Azure Synapse Analytics: Azure Synapse Analytics (formerly Azure SQL Data Warehouse) is a limitless analytics service that brings together enterprise data warehousing and big data analytics.
    - Azure Synapse pipelines leverages the capabilities of Azure Data Factory. It's the cloud-based ETL and data integration service that enables you to create data-driven workflows for orchestrating data movement, and transforming data at scale.
    - Use Azure Synapse Link to perform operational analytics with near real-time hybrid transactional and analytical processing.
    - Workload groups enable you to define the resources to isolate and reserve resources for its use.
    - Workload classification: Using T-SQL, you can create a workload classifier to map queries to a specific classifier. A classifier can define the level of importance of the request, so that it can be mapped to a specific workload group that has an allocation of specific resources during the execution of the query.
    - Workload importance: Workload importance is defined in the CREATE WORKLOAD CLASSIFIER command, and enables higher priority queries to receive resources ahead of lower priority queries that are in the queue. 
    - Result-set cache: Result-set cache enables interactive response times for repetitive queries against tables with infrequent data changes.
    - Materialized views: A materialized view can pre-compute, store, and maintain data like a table. These views are automatically updated when data in underlying tables are changed. Updating materialized views is a synchronous operation that occurs as soon as the data is changed.
    - Continuous Integration/Continuous Delivery (CI/CD) support through SQL Server Data Tools (SSDT).
    - SQL Pools: A SQL pool represents an abstract, normalized measure of compute resources and performance. By changing the service level, you alter the number of Data Warehouse Units (DWUs) that are allocated to the system, which in turn adjusts the performance, and thus the cost, of the system.
    - Control node: The control node is the brain of the data warehouse. It is the front end that interacts with all applications and connections. The MPP engine runs on the Control node to optimize and coordinate parallel queries. 
    - Compute nodes: The compute nodes provide the computational power. Distributions map to compute nodes for processing. As you pay for more compute resources, SQL Data Warehouse re-maps the distributions to the available compute nodes. The number of compute nodes ranges from 1 to 60 and is determined by the service level for the data warehouse.
    - Data Movement Service: Data Movement Service (DMS) is the data transport technology that coordinates data movement between the compute nodes. When SQL Data Warehouse runs a query, the work is divided into 60 smaller queries that run in parallel. Each of the 60 smaller queries runs on one of the underlying data distributions.
    - Azure Synapse Analytics supports these sharding patterns:
        - Round-robin distributed tables: A round-robin table is the most straightforward table to create and deliver fast performance when used as a staging table for loads. Data is distributed equally among all the 60 underlying distributions. There is no specific key used to distribute the data. This is the default method used when no data distribution strategy is specified.
        - Hash-distributed tables: A hash-distributed table can deliver the highest query performance for joins and aggregations on large tables. In the table definition, one of the columns is designated as the distribution column. The hash function uses the values in the distribution column to assign each row to a distribution.
        - Replicated tables: A replicated table provides the fastest query performance for small tables. A table that is replicated caches a full copy on each compute node. Consequently, replicating a table removes the need to transfer data among compute nodes before a join or aggregation. This requires extra storage and there are additional overheads that are incurred when writing data which make large tables impractical.
    - PolyBase is a technology that accesses external data stored in Azure Blob storage, Hadoop, or Azure Data Lake Store via the Transact-SQL language.

- Azure HDInsight: Azure HDInsight is a fully managed, open-source analytics service for enterprises. It's a cloud service that makes it easier, faster, and more cost-effective to process massive amounts of data. You can run popular open-source frameworks and create cluster types such as Apache Spark, Apache Hadoop, Apache Kafka, Apache HBase, Apache Storm, and Machine Learning Services.

- Azure Databricks: Azure Databricks helps you unlock insights from all your data and build artificial intelligence solutions. You can set up your Apache Spark environment in minutes, and then autoscale and collaborate on shared projects in an interactive workspace.

- Azure Data Lake Analytics: Azure Data Lake Analytics is an on-demand analytics job service that simplifies big data. Instead of deploying, configuring, and tuning hardware, you write queries to transform your data and extract valuable insights.

- Azure Stream Analytics: Azure Stream Analytics is a real-time analytics and complex event-processing engine that is designed to analyze and process high volumes of fast streaming data from multiple sources simultaneously.

- Azure Time Series Insights: Azure Time Series Insights is built to store, visualize, and query large amounts of time series data, such as that generated by IoT devices. If you want to store, manage, query, or visualize time series data in the cloud, Azure Time Series Insights is likely right for you.
    - Integrated with cloud gateways like Azure IoT Hub and Azure Event Hubs.
    - Provides out-of-the-box visualization through the Azure Time Series Insights Explorer.

- Azure Data Factory: Azure Data Factory (ADF) is an ELT tool for orchestrating data from different sources to the target. By Default, Azure Data Factory supports the extraction of data from different sources and different targets like SQL Server.
    - Copy Data Tool: The Azure Data Factory Copy Data tool eases and optimizes the process of ingesting data into a data lake, which is usually a first step in an end-to-end data integration scenario. It saves time, especially when you use Azure Data Factory to ingest data from a data source for the first time.
    - Pipeline: A pipeline is a logical grouping of activities that performs a unit of work. Together, the activities in a pipeline perform a task. For example, a pipeline can contain a group of activities that ingests data from an Azure blob, and then runs a Hive query on an HDInsight cluster to partition the data.
    - Mapping data flows: Create and manage graphs of data transformation logic that you can use to transform any-sized data. You can build-up a reusable library of data transformation routines and execute those processes in a scaled-out manner from your ADF pipelines. Data Factory will execute your logic on a Spark cluster that spins-up and spins-down when you need it. You won't ever have to manage or maintain clusters.
    - Activity: Activities represent a processing step in a pipeline. For example, you might use a copy activity to copy data from one data store to another data store. Similarly, you might use a Hive activity, which runs a Hive query on an Azure HDInsight cluster, to transform or analyze your data. Data Factory supports three types of activities: data movement activities, data transformation activities, and control activities.
    - Datasets: Datasets represent data structures within the data stores, which simply point to or reference the data you want to use in your activities as inputs or outputs.
    - Linked services: Linked services are much like connection strings, which define the connection information that's needed for Data Factory to connect to external resources. Think of it this way: a linked service defines the connection to the data source, and a dataset represents the structure of the data. For example, an Azure Storage-linked service specifies a connection string to connect to the Azure Storage account. Additionally, an Azure blob dataset specifies the blob container and the folder that contains the data.
    - Triggers: Triggers represent the unit of processing that determines when a pipeline execution needs to be kicked off. There are different types of triggers for different types of events.
    - Pipeline run: A pipeline run is an instance of the pipeline execution. Pipeline runs are typically instantiated by passing the arguments to the parameters that are defined in pipelines. The arguments can be passed manually or within the trigger definition.
    - Parameters: Parameters are key-value pairs of read-only configuration. Parameters are defined in the pipeline. The arguments for the defined parameters are passed during execution from the run context that was created by a trigger or a pipeline that was executed manually. Activities within the pipeline consume the parameter values.
    - Control flow: Control flow is an orchestration of pipeline activities that includes chaining activities in a sequence, branching, defining parameters at the pipeline level, and passing arguments while invoking the pipeline on-demand or from a trigger. It also includes custom-state passing and looping containers, that is, For-each iterators.
    - Variables: Variables can be used inside of pipelines to store temporary values and can also be used in conjunction with parameters to enable passing values between pipelines, data flows, and other activities.

- Power BI: Power BI is a unified self-service and enterprise analytics solution. It lets you visualize your data and share insights across your organization and embed them in your app or website. Azure Analytics and Power BI together provide insights at scale, allowing you to develop the data-driven culture needed to thrive in a fast-paced, competitive environment.

- Azure Analysis Services: Azure Analysis Services is a fully managed platform as a service (PaaS) that provides enterprise-grade data models in the cloud.

### Architect message brokering and serverless applications in Azure

- What is serverless compute: Serverless compute can be thought of as a function as a service (FaaS), or a microservice that is hosted on a cloud platform. Your business logic runs as functions and you don't have to manually provision or scale infrastructure.
    - Benefits of a serverless compute solution: Avoids over-allocation of infrastructure, Stateless logic, Event driven (triggers), Functions can be used in traditional compute environments
    - Drawbacks of a serverless compute solution: Execution time, Execution frequency
    - Bindings: Bindings are a declarative way to connect data and services to your function. Bindings know how to talk to different services, which means you don't have to write code in your function to connect to data sources and manage connections.

- Azure Logic Apps: Azure Logic Apps gives you pre-built components to connect to hundreds of services. You put the pieces together in any combination you need. 
    - Logic Apps components:
        - A trigger is an event that occurs when a specific set of conditions is satisfied. Triggers activate automatically when the conditions are right. For example, when a timer expires or data becomes available. Every logic app must start with a trigger. In our example, we'll trigger the app when a new tweet mentions our product.
        - An action is an operation that executes one of the tasks in your business process. Actions run when a trigger activates or another action completes. Our social-media monitor app has three actions: detect sentiment, insert database row, and send email.
        - Control actions are special built-in actions that let you add decisions and loops to your app. Our example will use a control action to branch based on the sentiment score.
    - Trigger types:
        - A polling trigger periodically checks an external service for new data. For example, the trigger that looks for new posts in an RSS feed is implemented using polling.
        - A push trigger subscribes to an event offered by the external service to get notified immediately when data is available. For example, the trigger that detects when a message is added to an Azure Service Bus queue is a push trigger.
    - Trigger parameters let you configure the operation. Trigger return values are the results of the operation.
    - Action types:
        - Access external services, for example Salesforce, Oracle, YouTube, Dropbox, Gmail, GitHub, Twilio, Facebook, Slack, and Jira.
        - Data operation actions let you work with the data that you pull into your logic app. There are operations to concatenate multiple values into a single string, parse JSON data, select particular values from an array, and so on.
        - Alter control flow: The control action feature of Logic Apps lets you add control constructs like conditional statements and loops to your app.

- Azure Service Bus
    - Service Bus is intended for traditional enterprise applications. These enterprise applications require transactions, ordering, duplicate detection, and instantaneous consistency.
    - Supports larger messages sizes of 256 KB (standard tier) or 1MB (premium tier) per message versus 64 KB
    - Supports role-based security
    - Azure Queue Storage: Queue storage is a service that uses Azure Storage to store large numbers of messages that can be securely accessed from anywhere in the world using a simple REST-based interface. Queues can contain millions of messages, limited only by the capacity of the storage account that owns it.
        - A message in a queue is a byte array of up to 64 KB. Message contents are not interpreted at all by any Azure component.
        - The combination of storage account name and queue name uniquely identifies a queue.
        - The queue will handle spikes in traffic and ensure no data is lost. If the VM cannot keep up with the flow of incoming messages, it will process the message backlog during low-traffic times.
        - By design, messages are not automatically deleted from a queue after they are retrieved for processing. This helps ensure that every message is processed to completion. 
        - Use Queue storage if you:
            - Need an audit trail of all messages that pass through the queue.
            - Expect the queue to exceed 80 GB in size.
            - Want to track progress for processing a message inside of the queue.
    - Azure Service Bus Queues: Service Bus is a message broker system intended for enterprise applications. These apps often utilize multiple communication protocols, have different data contracts, higher security requirements, and can include both cloud and on-premises services. Service Bus is built on top of a dedicated messaging infrastructure designed for exactly these scenarios.
        - Use Service Bus topics if you:
            - Need multiple receivers to handle each message
    - Azure Service Bus topics are like queues, but can have multiple subscribers. When a message is sent to a topic instead of a queue, multiple components can be triggered to do their work.
        - Benefits of queues: Increased reliability, Message delivery guarantees, Transactional support.
        - Message delivery guarantees:
            - At-Least-Once Delivery: In this approach, each message is guaranteed delivery to at least one of the components that retrieve messages from the queue. 
            - At-Most-Once Delivery: In this approach, each message is not guaranteed for delivery, and there is a small chance that it may not arrive.
            - First-In-First-Out (FIFO): In most messaging systems, messages usually leave the queue in the same order in which they were added, but you should consider whether this delivery is guaranteed.
        - Use Service Bus queues if you:
            - Need order processing and financial transactions
            - Need an At-Most-Once delivery guarantee.
            - Need a FIFO guarantee.
            - Need to group messages into transactions.
            - Want to receive messages without polling the queue.
            - Need to provide a role-based access model to the queues.
            - Need to handle messages larger than 64 KB but less than 256 KB.
            - Queue size will not grow larger than 80 GB.
            - Want to publish and consume batches of messages.

- Azure Event Grid: Azure Event Grid is a fully-managed event routing service running on top of Azure Service Fabric. Event Grid distributes events from different sources, such as Azure Blob storage accounts or Azure Media Services, to different handlers, such as Azure Functions or Webhooks. Event Grid was created to make it easier to build event-based and serverless applications on Azure.
    - Event Grid is an eventing backplane that enables event-driven, reactive programming. It uses a publish-subscribe model. Publishers emit events, but have no expectation about which events are handled. Subscribers decide which events they want to handle.
    - Event Grid supports most Azure services as a publisher or subscriber and can be used with third-party services.
    - Events are the data messages passing through Event Grid that describe what has taken place. Each event is self-contained, can be up to 64 KB, and contains several pieces of information based on a schema defined by Event Grid.
    - Event sources are responsible for sending events to Event Grid. Each event source is related to one or more event types. For example, Azure Storage is the event source for blob created events.
    - Event topics categorize events into groups. Topics are represented by a public endpoint and are where the event source sends events to.
        - System topics are built-in topics provided by Azure services. You don't see system topics in your Azure subscription because the publisher owns the topics, but you can subscribe to them.
        - Custom topics are application and third-party topics. When you create or are assigned access to a custom topic, you see that custom topic in your subscription.
    - An event handler (sometimes referred to as an event "subscriber") is any component (application or resource) that can receive events from Event Grid.
    - Choose Event Hubs if:
        - You want to do reactive programming
        - You need to support authenticating a large number of publishers.
        - You need to save a stream of events to Data Lake or Blob storage.
        - You need aggregation or analytics on your event stream.
        - You need reliable messaging or resiliency.

- Azure Event Hubs: Azure Event Hubs is a cloud-based, event-processing service that can receive and process millions of events per second. Event Hubs acts as a front door for an event pipeline, to receive incoming data and stores this data until processing resources are available.
    - Data sent to an event hub can be transformed and stored by using any real-time analytics provider or batching/storage adapters.
    - Event Hubs provides an endpoint compatible with the Apache Kafka producer and consumer APIs that can be used by most existing Apache Kafka client applications as an alternative to running your own Apache Kafka cluster.
    - Event Hubs also provides the Shared Access Signatures (SAS) for delegated access to Event Hubs for Kafka resources. Authorizing access using OAuth 2.0 token-based mechanism provides superior security and ease of use over SAS.
    - Capture your data in near-real time in an Azure Blob storage or Azure Data Lake Storage for long-term retention or micro-batch processing. 
    - An entity that sends data to the Event Hubs is called a publisher, and an entity that reads data from the Event Hubs is called a consumer or a subscriber.
    - An event is a small packet of information (a datagram) that contains a notification. Events can be published individually, or in batches, but a single publication (individual or batch) can't exceed 1 MB.
    - Event publishers are any app or device that can send out events using either HTTPS or Advanced Message Queuing Protocol (AMQP) 1.0.
    - An Event Hub consumer group represents a specific view of an Event Hub data stream. By using separate consumer groups, multiple subscriber apps can process an event stream independently, and without affecting other apps.
    - More info: https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about
    - Use Event Hubs if you:
        - Need low latency
        - Need at least once delivery
        - You want receiving and processing millions of events per second
    - Event Hubs can be combined with Event Grid. More info: https://docs.microsoft.com/en-us/azure/event-grid/compare-messaging-services

- Azure IoT Hub: Azure IoT Hub provides a cloud-hosted solution back end to connect virtually any device. Extend your solution from the cloud to the edge with per-device authentication, built-in device management and scaled provisioning.
    - Supports additional protocols: MQTT, MQTT over webSockets
    - Supports 2-way communication to IOT enabled devices

- Azure Relay: Azure Relay gives you a way to connect services across network boundaries and firewalls, without having to reconfigure your security setup.
    - You can make two types of connections in Azure Relay:
        - Hybrid connections: Hybrid connections are two-way streams of binary data that use either WebSocket or HTTP standards.
            - Hybrid connections can use one of these protocols:
                - HTTP: This stateless protocol consists of requests such as GET and POST, and it's used to transfer webpages between web servers and browsers. Usually, HTTP uses TCP port 80 or 443 when the request is secured with Secure Sockets Layer.
                - WebSocket: This protocol creates a full duplex communication channel over port 80 or 443, which is more efficient than the stateless HTTP protocol. A WebSocket connection is especially efficient when the communication consists of many messages, not just a single request and response.
        - WCF connections: Some developers use Windows Communication Foundation (WCF) to enable remote procedure calls. WCF was commonly used for network communications with older versions of the .NET Framework. WCF is now considered a legacy protocol, but it remains in common use in older applications.

### Architect modern applications in Azure

- Docker: Docker is a tool for running containerized apps. A containerized app includes the app and the filesystem that makes up the environment in which it runs.
    - Docker images are stored and made available in registries. A registry is a web service to which Docker can connect to upload and download container images. The most well-known registry is Docker Hub, which is a public registry.
    - A registry is organized as a series of repositories. Each repository contains multiple Docker images that share a common name and generally the same purpose and functionality. These images normally have different versions identified with a tag.

- Azure Container Instances: Azure Container Instances is useful for scenarios that can operate in isolated containers, including simple applications, task automation, and build jobs.
    - Very useful for very basic or burst scenarios.
    - Can be integrated with AKS via Virtual Kubelet.
    - Environment variable are not secured by default and their values can be seen in the Azure portal and the Azure CLI output.
    - The restart policy Always will ensure needed processes continue to be available even if a restart is required.
    - Here are some of the benefits:
        - Fast startup: Launch containers in seconds.
        - Per second billing: Incur costs only while the container is running.
        - Hypervisor-level security: Isolate your application as completely as it would be in a VM.
        - Custom sizes: Specify exact values for CPU cores and memory.
        - Persistent storage: Mount Azure Files shares directly to a container to retrieve and persist state.
        - Linux and Windows: Schedule both Windows and Linux containers using the same API.

- Azure Container Registry: Azure Container Registry is a managed Docker registry service based on the open-source Docker Registry 2.0. Container Registry is private, hosted in Azure, and allows you to build, store, and manage images for all types of container deployments.
    - Azure Container Registry is a private registry. Images cannot be accessed without authentication.
    - Azure service principals are the recommended authentication method. They provide granular access to container images in Azure Container Registry; for example, you can specify read-only access or full access to the container registry.
    - Placing a registry in each region that runs the images will ensure network-close registry access everywhere it is needed.
    - Can be GEO-replicated (with Premium SKU)
    - Can also run jobs to create images.

- Azure App Service: Azure App Service is a fully managed web application hosting platform. Azure App Service enables you to build and host web applications in the programming language of your choice without managing infrastructure.
    - App Service plans: An App Service plan is a set of virtual server resources that run App Service apps. A plan's size (sometimes referred to as its sku or pricing tier) determines the performance characteristics of the virtual servers that run the apps assigned to the plan and the App Service features that those apps have access to.
        - Every App Service web app you create must be assigned to a single App Service plan that runs it.
        - More information about pricing and different SKUs: https://azure.microsoft.com/en-us/pricing/details/app-service/windows/
        - Multiple applications can be deployed to the same plan (shared resources)
    - Deployment slots: Deployment slots are live apps with their own hostname. App content and settings can be easily swapped.
    - Continuous integration/deployment support: Azure App Service provides out-of-the-box continuous integration and deployment with Azure DevOps, GitHub, Bitbucket, FTP, or a local Git repository on your development machine.
    - Integrated Visual Studio publishing and FTP publishing.
    - Built-in auto scale support for plans (automatic scale-out based on real-world load)
    - Support for Docker images
    - Supports service endpoints (restrict access certain subnets)
    - App Service Environment (ASE) dedicated deployment into your VNet.
        - The Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale. ASEs host applications from only one customer and do so in one of their VNets. Customers have fine-grained control over inbound and outbound application network traffic. 
    - Hybrid Connections: Within App Service, Hybrid Connections can be used to access application resources in any network that can make outbound calls to Azure over port 443. Hybrid Connections provides access from your app to a TCP endpoint and does not enable a new way to access your app. As used in App Service, each Hybrid Connection correlates to a single TCP host and port combination. This enables your apps to access resources on any OS, provided it is a TCP endpoint. The Hybrid Connections feature does not know or care what the application protocol is, or what you are accessing. It simply provides network access. More info: https://docs.microsoft.com/en-us/azure/app-service/app-service-hybrid-connections

- Azure Static Web Apps: Azure Static Web Apps is a service that automatically builds and deploys full stack web apps to Azure from a code repository.
    - Static web apps are commonly built using libraries and frameworks like Angular, React, Svelte, Vue, or Blazor where server side rendering is not required. These apps include HTML, CSS, JavaScript, and image assets that make up the application. 

- WebJobs: WebJobs are a feature of Azure App Service that lets you run arbitrary programs or scripts using the same App Service Plan resources as a web app. WebJobs can be used to run any script or console application that can be run on a Windows computer, with some functionality limitations.
    - WebJobs can be written as scripts of several different kinds including Windows batch files, PowerShell scripts, or Bash shell scripts. Alternatively, you can write WebJobs using a framework such as Python or Node.js.
    - There are two types of WebJobs, which execute at different times:
        - Continuous. A continuous WebJob starts when you deploy it and will continue to run in an endless loop. If you want to use a continuous WebJob, you must write your code to implement this loop. You could use this kind of WebJob, for example, to poll a message queue for new items and process their contents. Because the WebJob is continuous, your process can start quickly after the message appears.
        - Triggered. A triggered WebJob only starts when scheduled or manually triggered. You could use this kind of WebJob, for example, to create daily summaries of messages in a queue.

- Azure Kubernetes Service: Azure Kubernetes Service (AKS) manages your hosted Kubernetes environment and makes it simple to deploy and manage containerized applications in Azure.
    - When more complex orchestration is required, for example complex networking, scaling, service communication, and so on.
    - Azure Dev Spaces: Azure Dev Spaces helps your development teams be more productive on Kubernetes and allows you to:
        - Minimize the local dev machine setup for each team member as developers can work directly in AKS
        - Rapidly iterate and debug code directly in Kubernetes using Visual Studio or Visual Studio Code
        - Generate Docker and Kubernetes configuration-as-code assets to use from development through to production
        - Develop your code in isolation, and do integrated testing with other components without replicating or mocking up dependencies
    - Deployment Center: Deployment center simplifies setting up a DevOps pipeline for your application. You can use this configured DevOps pipeline to set up a continuous integration (CI) and continuous delivery (CD) pipeline to your AKS Kubernetes cluster.
    - Azure Service Integration: AKS allows us to integrate any Azure service offering and use it as part of an AKS cluster solution.
    - You only pay for the virtual machines instances, storage, and networking resources consumed by your Kubernetes cluster.
    - AKS supports both static and dynamic storage volumes for containers that need persisted storage.
    - Supports Managed Identities
    - User node pools can use spot instances (cheap compute)
    - Can use Azure Container Instances for burst via AKS virtual kubelet.

- Azure Service Fabric: Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers. Service Fabric also addresses the significant challenges in developing and managing cloud native applications.
    - A key differentiator of Service Fabric is its strong focus on building stateful services. You can use the Service Fabric programming model or run containerized stateful services written in any language or code. 
    - You can create Service Fabric clusters anywhere, including Windows Server and Linux on premises and other public clouds, in addition to Azure.

### Architect API integration in Azure

- Azure API management: The Azure API management service is hosted in the Azure cloud and is positioned between your APIs and the Internet. An Azure API gateway is an instance of the Azure API management service.
    - For developers, API Management provides a range of benefits:
        - API documentation. Documentation of APIs enables calling clients to quickly integrate their solutions. API Management allows you to quickly expose the structure of your API to calling clients through modern standards like Open API. You can have more than one version of an API. With multiple versions, you can stage app updates as your consuming apps don't have to use the new version straight away.
        - Rate limiting access. If your API could potentially access a large amount of data, it's a good idea to limit the rate at which clients can request data. Rate limiting helps maintain optimal response times for every client. API Management let you set rate limits as a whole or for specific individual clients.
        - Health monitoring. APIs are consumed by remote clients. So it can be difficult to identify potential problems or errors. API Management lets you view error responses and log files, and filter by types of responses.
        - Modern formats like JSON. APIs have used many different data exchange formats over the years from XML to CSV and many more. API Management enables you to expose these formats using modern data models like JSON.
        - Connections to any API. In many businesses, APIs are located across different countries and use different formats. API Management lets you add all of these disparate APIs into single modern interface.
        - Analytics. As you develop your APIs, it's useful to see how often your APIs are being called and by which types of systems. API Management allows you to visualize this data within the Azure portal.
        - Security. Security is paramount when dealing with system data. Unauthorized breaches can cost companies money, time lost in reworking code, and reputational loss. Security tools that you can use with Azure API management include OAuth 2.0 user authorization, and integration with Azure Active Directory.
    - Policies can be used to secure all your endpoints.
    - Subscription keys form the authorization to enable access to these subscriptions. Whenever a client makes a request to a protected API, they must include a valid subscription key in the HTTP request or the call will be rejected.
    - Certificates can be used to provide TLS mutual authentication between the client and the API gateway.

### Architect migration, business continuity, and disaster recovery in Azure

- Azure migration framework: You can use a framework of Assess, Migrate, Optimize, and Monitor as a path for migration. Each stage focuses on a particular aspect of ensuring the success of a migration.
    - For each application, there are multiple migration options:
        - Rehost: Recreate your existing infrastructure in Azure. Choosing this approach has the least impact because it requires minimal changes. It typically involves moving virtual machines from your data center to virtual machines on Azure.
        - Refactor: Move services running on virtual machines to platform-as-a-service (PaaS) services. This approach can reduce operational requirements, improve release agility, and keep your costs low. Small enhancements to run more efficiently in the cloud can have large impacts on performance.
        - Rearchitect: You might be forced to rearchitect some systems so that they can be migrated. Other apps could be changed to become cloud native, or to take advantage of new approaches to software, such as containers or microservices.
        - Rebuild: You might need to rebuild software if the cost to rearchitect it is more than that of starting from scratch.
        - Replace: While you're reviewing your estate, it's possible you'll find that third-party applications could completely replace your custom applications. Evaluate software-as-a-service (SaaS) options that can be used to replace existing applications.

- Azure Migrate: Azure Migrate is a free service, provided by Microsoft, that discovers, assesses, and migrates on-premises systems to Azure. The service helps with performance-based sizing calculations (virtual machine sizing, compute/storage) for the machines that you'll migrate and estimate the ongoing cost of running these machines in Azure.
    - Assess Azure readiness, obtain VM size recommendations, migrate with confidence
    - Server Assessment tool guides you through downloading a lightweight collector appliance, which carries out the discovery of systems in your environment. The collector appliance is available to download to VMware or Hyper-V environment. Import and spin up the collector appliance, and then complete its configuration to connect it to the Azure Migrate project.
    - Order of steps to complete an Azure readiness assessment: Install the collector appliance on the vCenter Server, install dependency agents on each on-premises VM, create the assessment, and then edit the default properties of the assessment to your requirements.
    - Virtual machine replication
        - Supports Azure VMs, VMware VMs, Hyper-V VMs, Physical Windows
        - You can only replicate up to 100 at a time.
    - Azure Database Migration Service: Azure Database Migration Service enables online and offline migrations from multiple database sources to Azure data platforms, all with minimal downtime.
        - Your relational database can be migrated to a number of different destinations in Azure:
            - Single Azure SQL Database instance: A fully managed, single SQL database.
            - Azure SQL Database managed instance: 100% compatible with SQL Server Enterprise Edition Database Engine, but missing some minor SQL Server features.
            - SQL Server on Azure Virtual Machines: An infrastructure-as-a-service (IaaS) offering that runs a full version of SQL Server and supports all the features of SQL Server.
            - Azure Database for MySQL: An Azure database service based on the MySQL Community Edition, versions 5.6 and 5.7.
            - Azure Database for PostgresSQL: An Azure database service based on the community version of the PostgreSQL database engine.
            - Azure Cosmos DB: A globally distributed, multi-model, fully managed database service.
        - Requires CONTROL SERVER, CONTROL DATABASE roles
        - Only SQL Server on Azure Virtual Machines guarantees 100% compatibility

- Azure Site Recovery: Azure Site Recovery (ASR) replicates workloads between a primary and secondary site.
    - Azure Site Recovery (ASR) is a disaster recovery solution for physical servers. The physical server–based environment can be replicated to Azure using ASR. The same approach can be used for migration, where the replicated environment is failed over and then continues to run from Azure.
    - Offers two solutions for on-premises to Azure:
        - Hyper-V replication to Azure: Hyper-V VMs - Hyper V replica
        - VMWare or physical via Mobility service (in-guest). The Mobility service captures data writes on the machine, and forwards them to the Site Recovery process server.
    - Azure to Azure disaster recovery architecture: use Multi-VM consistency groups to replicate VMs together.
    - Business continuity and disaster recovery: BCDR plans are formal documents that companies draw up that cover the scope and actions to be taken when a disaster or large-scale outage happens.
    - Recovery time objective: An RTO is a measure of the maximum amount of time your business can survive after a disaster before normal service is restored.
    - Recovery point objective: An RPO is a measure of the maximum amount of data loss that's acceptable during a disaster.
    - Key steps required: Networking, create a Recovery Services vault, give the correct permissions to credentials, install a configuration server in your vCenter via an OVA
    - Proving the recovery on a single VM, on an isolated network, ensures that live services aren't affected and proves the recoveries are set up correctly.
    - SQL Server Always On is a flexible design solution to provide high availability (HA) and disaster recovery (DR): App-consistent snapshots, near synchronous replication, SQL Server Always On integration
    - Azure Site Recovery supported workloads:
        - Azure VM: Replication is available for any workload that runs on a supported Azure virtual machine.
        - Hyper-V VM: Protection is available for any workload that runs on a Hyper-V virtual machine.
        - Physical servers: Protection is available for Windows and Linux operating systems.
        - VMware VM: Protection is available for any workload that runs in a VMware virtual machine.
    - Active Directory and DNS can be configured for an automated failover.
    - Site Recovery can be used alongside SQL-specific high-availability technologies, such as Always On availability groups.
    - For IIS: One-click failover, script integration, network mapping
    - Disaster recovery drill: a full disaster recovery test without affecting your existing live environment
    - Site recovery dashboard statistics include: Replicated items, monitoring of test failovers, and monitoring of configuration issues.
    - Failover and failback: A failover is the process that takes place when the decision is made to invoke the BCDR plan for the business. A failback is the reverse of a failover. The previous live environment (which is now the replica environment because a failover took place) takes back its original role and becomes the live environment again.
    - Four stages of failover and failback: 1) Fail over to the secondary site on Azure. 2) Reprotect the Azure virtual machines by replicating back to on-premises. 3) Fail back to the primary on-premises site. 4) Reprotect the on-premises virtual machines by replicating to Azure.
    - Cloud Witness: Microsoft Cloud Witness is a high availability (HA) feature for failover clusters that uses storage in the Microsoft Azure cloud platform to ensure clusters continue to function if there is a site outage.

- Azure Backup: Azure Backup is a built-in Azure service that provides secure backup for all Azure-managed data assets. It uses zero-infrastructure solutions to enable self-service backups and restores, with at-scale management at a lower and predictable cost.
    - Azure Backup versus Azure Site Recovery: Azure Backup does scheduled backup of VMs at specified time intervals to address the data and application resiliency concerns of environments hosted in Azure. If you have stringent recovery time objectives (RTOs) and recovery point objectives (RPOs) defined in a business continuity and disaster recovery (BCDR) strategy, Azure Site Recovery (ASR) could be the better choice because it replicates data continuously to a different region in Azure.
    - Azure Backup supported scenarios:
        - Azure VMs - Back up Windows or Linux Azure virtual machines
        - On-premises - Back up files, folders, and system state using the Microsoft Azure Recovery Services (MARS) agent. Or use Microsoft Azure Backup Server (MABS) or Data Protection Manager (DPM) server to protect on-premises VMs (Hyper-V and VMWare) and other on-premises workloads.
        - Azure Files shares - Azure Files - Snapshot management by Azure Backup
        - SQL Server in Azure VMs and SAP HANA databases in Azure VMs
        - Recovery Services vault: Azure Backup uses a Recovery Services vault to manage and store the backup data. A vault is a storage-management entity, which provides a simple experience to carry out and monitor backup and restore operations.
        - Snapshots: A snapshot is a point-in-time backup of all disks on the virtual machine.
        - Backup policy: frequency and retention duration for your backups. Snapshot tier: All the snapshots are stored locally for a maximum period of five days. Vault tier: All snapshots are additionally transferred to the vault for additional security and longer retention.
        - If the VM was deleted, the disk can't be restored.
        - Selecting replace existing disk to allow for a disk to be restored and then used to replace a disk on an existing VM.
    - Snapshot consistency:
        - App-consistent backups capture memory content and pending I/O operations. App-consistent snapshots use a VSS writer (or pre/post scripts for Linux) to ensure the consistency of the app data before a backup occurs.
        - File-system consistent backups provide consistency by taking a snapshot of all files at the same time.
        - Crash-consistent snapshots typically occur if an Azure VM shuts down at the time of backup. Only the data that already exists on the disk at the time of backup is captured and backed up.
    - Azure Backup offers longer retention than Azure Site Recovery.
    - MARS Agent: Azure Backup uses the MARS agent to back up data from on-premises machines and Azure VMs to a backup Recovery Services vault in Azure. 

- Azure StorSimple: StorSimple is a hybrid device that helps enterprises consolidate their storage infrastructure for primary storage, data protection, archiving, and disaster recovery on a single solution by tightly integrating with Azure storage.

- Azure SQL Database: Protect the data in your Azure SQL database and recover from data loss or corruption with backup and restore.
    - Azure SQL Database uses SQL Server technology to make these types of backups:
        - Full backups: In a full backup, everything in the database and the transaction logs is backed up. SQL Database makes a full backup once a week.
        - Differential backups: In a differential backup, everything that changed since the last full backup is backed up. SQL Database makes a differential backup every 12 hours.
        - Transactional backups: In a transactional backup, the contents of the transaction logs are backed up. SQL Database makes a transaction log backup every 5 to 10 minutes. Transactional backups enable administrators to restore up to a specific time, which includes the moment before data was mistakenly deleted.
    - Long-term backup retention policies: Azure SQL Database automatic backups remain available to restore for up to 35 days. Use the long-term retention (LTR) feature for backups in read-access geo-redundant storage (RA-GRS) blobs for up to 10 years.

- Virtual machine scale set: Virtual machine scale sets in Azure are designed to allow you to deploy and manage many load-balanced, identical VMs. These machines run with the same configurations. Virtual machine scale sets are intelligent enough to automatically scale up or down the number of VM instances. A scale set can also change the size of VM instances.
    - In a low-priority scale set, you specify two kinds of removal:
        - Delete: The entire VM is removed, including all of the underlying disks.
        - Deallocate: The VM is stopped. The processing and memory resources are deallocated. Disks are left intact and data is kept. You're charged for the disk space while the VM isn't running.
    - Support spot instances.
    - Scale-In Policy: you can tune the deletion of virtual machines. For example ‘OldestVM’ to ‘NewestVM’. More info: https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-scale-in-policy
    - Supports termination notification: Scale set instances can opt in to receive instance termination notifications and set a pre-defined delay timeout to the terminate operation. More info: https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-terminate-notification
    - Instance protection: You can protect on virutal machine from deletion. More info: https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-instance-protection

- Azure App Service Autoscaling: Autoscaling in Azure App Service monitors the resource metrics of a web app as it runs. It detects situations where additional resources are required to handle an increasing workload, and ensures those resources are available before the system becomes overloaded.
    - Autoscaling is a scale out/scale in solution. The system can scale out when specified resource metrics indicate increasing usage, and scale in when these metrics drop.
    - Autoscaling works by adding or removing web servers.
    - Autoscaling provides elasticity for your services.
    - Autoscaling improves availability and fault tolerance.
    - The number of instances of a service is also a factor.
    - Autoscaling isn't the best approach to handling long-term growth.
    - The metrics you can monitor for a web app are:
        - CPU Percentage. This metric is an indication of the CPU utilization across all instances. A high value shows that instances are becoming CPU-bound, which could cause delays in processing client requests.
        - Memory Percentage. This metric captures the memory occupancy of the application across all instances. A high value indicates that free memory could be running low, and could cause one or more instances to fail.
        - Disk Queue Length. This metric is a measure of the number of outstanding I/O requests across all instances. A high value means that disk contention could be occurring.
        - Http Queue Length. This metric shows how many client requests are waiting for processing by the web app. If this number is large, client requests might fail with HTTP 408 (Timeout) errors.
        - Data In. This metric is the number of bytes received across all instances.
        - Data Out. This metric is the number of bytes sent by all instances.
    - The autoscale rule will not trigger the action again until the cool down period for the rule has expired. If the disk queue length is still over 10 at this time, the action will be performed.

- Azure DNS: Azure DNS provides name resolution entirely through the Azure infrastructure. This service is inherently multi-regional, and that's why there's no need to modify our existing Azure DNS configuration to support the feature in our new architectural design.
    - The Azure-created DNS suffix cannot be modified.
    - All PTR queries for IP addresses of virtual machines will return FQDNs of form [vmname].internal.cloudapp.net
    - The Azure DNS IP address is 168.63.129.16. This is a static IP address and will not change.

- Azure Front Door: Azure Front Door is a global, scalable entry-point that uses the Microsoft global edge network to create fast, secure, and widely scalable web applications. With Front Door, you can transform your global consumer and enterprise applications into robust, high-performing personalized modern applications with contents that reach a global audience through Azure.
    - Front Door works at Layer 7 (HTTP/HTTPS layer) using anycast protocol with split TCP and Microsoft's global network to improve global connectivity. Based on your routing method you can ensure that Front Door will route your client requests to the fastest and most available application backend.
    - Similar to Azure Application Gateway, but Azure Front Door is Global.
    - If you want to load balance between your servers in a region at the application layer, review Azure Application Gateway.
    - To do network layer load balancing, review Azure (Global) Load Balancer.

- Azure CDN: The Azure CDN service is a global network of servers that caches static content close to users.

- Azure Redis Cache: Azure Cache for Redis is a fully managed, in-memory cache that enables high-performance and scalable architectures.

- Azure Cost Management + Billing: Azure Cost Management + Billing is a suite of tools provided by Microsoft that help you analyze, manage, and optimize the costs of your workloads. Using the suite helps ensure that your organization is taking advantage of the benefits provided by the cloud.
    - Azure Billing features are used to review your invoiced costs and manage access to billing information. In larger organizations, procurement and finance teams usually conduct billing tasks.
    - Cost Management shows organizational cost and usage patterns with advanced analytics. Reports in Cost Management show the usage-based costs consumed by Azure services and third-party Marketplace offerings. Costs are based on negotiated prices and factor in reservation and Azure Hybrid Benefit discounts. Collectively, the reports show your internal and external costs for usage and Azure Marketplace charges.
    - Azure Pricing Calculator: Use this tool to estimate your up-front cloud costs.
    - Azure Migrate: Assess your current datacenter workload for insights about what's needed from an Azure replacement solution.
    - Azure Advisor: Identify unused VMs and receive recommendations about Azure reserved instance purchases.
    - Azure Hybrid Benefit: Use your current on-premises Windows Server or SQL Server licenses for VMs in Azure to save.
    - Azure Budgets in Subscriptions: Budgets in Cost Management help you plan for and drive organizational accountability. With budgets, you can account for the Azure services you consume or subscribe to during a specific period. They help you inform others about their spending to proactively manage costs, and to monitor how spending progresses over time.

- Azure Automation: Azure Automation is a new service in Azure that allows you to automate your Azure management tasks and to orchestrate actions across external systems from right within Azure. It is built on PowerShell Workflow, so you can take advantage of the language’s many features.
    - Configuration Management in Azure Automation allows access to two features:
        - Change Tracking: Change Tracking and Inventory combines change tracking and inventory functions to allow you to track virtual machine and server infrastructure changes.
        - Inventory and Azure Automation State Configuration: Azure Automation State Configuration is a cloud-based feature for PowerShell desired state configuration (DSC) that provides services for enterprise environments. Using this feature, you can manage your DSC resources in Azure Automation and apply configurations to virtual or physical machines from a DSC pull server in the Azure cloud.
    - Runbooks: Runbooks are PowerShell workflows. In a nutshell those are a mix of PowerShell scripts and Workflow Foundation (WF) worflows. They allow long running workflows, pauses, restart, etc.
