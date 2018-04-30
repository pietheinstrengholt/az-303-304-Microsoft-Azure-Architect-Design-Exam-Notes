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

### Role-Based Security
- Concept is to give roles access rights and assign the roles to groups and users.
- Standard roles: owner, contributor, reader (read only)
- Access inheritance. Azure subscription belongs to only one AAD. Azure group belongs to only one subscription. Resource belongs only to one group. 

### Azure Data Storage
- Table Storage: Structured, Schemaless, name-value pair storage (no RDBMS!). Rows are called entities. PartionKey + RowKey are the primairy key. Entities can have up to 255 properties (columns). Timestamp is always included. 
- SQL Storage: Relational SQL storage. Elastic and auto-scales. Azure hosted database. Geo-replication (optional).
- DocumentDB Storage: NoSQL storage for JSON objects.
- Blob Storage: Container model, Containers have security. Blob = binary large object. 500TB capacity. Block blobs: Optimized for streaming and storing objects in the Cloud. Append blobs: Similar to block blobs but optimized for append only (log files). Page blobs: Good for random writes, represents harddisk, virtual machine storage.
- Queue Storage: Max 64gb in size. Invisibility behavior, read and then becomes invisible for a period of time.
- File Storage: Works as a network file share (SMB 3.0). Also a REST API. Useful for legacy systems. Can create directories. Each file can be up to 1TB. Files are addressable by a private URL.
- SQL Server VM: IaaS model for SQL Server. Needs a license.
- Securing SQL Server: By default only the owner of the storage account has access. Assign right roles. Avoid anonymous access. Whitelist IP's and use ACL (Access control lists). Encryption (can use SSL as well). Shared Access Signature (SAS) can give temporary access to storage. Shared Access Policy (SAP) can be given to users and revoked as needed.

### Azure Mobile Apps
- Azure Mobile Apps: Provides capabilities (PaaS services) to make the development of Mobile Apps much more easy.
- Cross Platform Applications: Cross platform support (Windows, iOS, Andriod, HTML5, Xamarin, Apache Cordova.
- Offline Sync: allows to use the mobile app offline and sync mobile client data once it becomes online. Uses implicit push and incremental pull model.
- Extend Mobile Apps: Services to provide essential functions for mobile apps, such as custom authentication push, notifications, data storage.
- Security: Two levels: Infrastrcture and platform security, Application Security. Infrastrcture and platform security = managed by Microsoft. Application Security = responsibility of developer.

### Azure Notification Hub
- Service that takes care of all the platforms (iOS, Android, Windows Mobile, Kindle). Uses single API. Also supports .NET, PHP, Java, NodeJS. Can target single user, group or all users. Allows tagging for sementation. Can security notification, so the app pulls the data secure after receiving the notification.

### Web API
- Web API: Web API is a way to communicate between to systems using API's. Web API runs on the MVC model. Verifies the request and populates a result based on the model. Can be deployed to a VM running IIS (IaaS) or to the PaaS Web Application. Integrated with Visual Studio.
- Scaling Web API: For the vm you can either, upgrade to a higher hosting place, change the tier, instance size and instance count (horizontal scaling). Can be used with traffic manager to grow across regions and geos.
- Web Jobs: continuously running jobs or predefined scheduled jobs. Works with Azure Service Bus or Azure Storage. Windows EXE, CMD, BAT, PS1, Shell, PHP, Python, NodeJS. Can scale by having more instances. Uses the WebJobs SDK.
- Securing Web API's: For corporate networks use Azure AD Service, AD Federation or Access Control Service. Monitoring or tokens. Audit, logging, validation of inputs, SSL or cryptographic. 

### Hybrid Applications
- Service Bus Relay: Alles apps to connect to your on premises services. The Service Bus Relay runs in the cloud accepts the request and securely passes on that request to the WCF service running indside the corp network.

### Azure Media Services
- Azure Media Services: Supports online streaming of video's for live and recorded. PaaS model, so no access to underlying hardware. Supports live encoding. Uses streaming endpoints. Supports previews, Media indexer for closed captions and transcripts. Checks quality of the stream. Archive and DRM (AES Clear Key dynamic encryption).

### Compute Intensive Applications
- For jobs that can not be handled sequential
- Managed, Scalable, Elastic and Pay for use model.
- HPC pack: on premises, hybrid or IaaS (spin up VM's) or PaaS (Azure Batch)
- Head node (controls the distribution of the jobs, can be on prem or cloud) and Compute nodes (execution of tasks)
- Azure Batch: Job scheduling as a service, application lifecycle management, budget, quotas, users and limites.

### Designing Long Running Applications
- Jobs that take days, weeks, with the risk of interupption.
- Availability: Multiple instances, stateless vs state-ful, avoid single point of failures, deploy across regions
- Reliability: Faultu domains, error handling and retry, loose coupling, monitoring
- Scaling: planned versus reactive. Scaling up versus out, breaking up into smaller parts
- Other considerations: partition the workload, Logging, Retry on errors, Gracefully restart, check points, single instances (is_singleton:true)

### Selecting Storage Options
- Traditional SQL have challenges around scaling, consider partioning and sharding.
- NoSQL options for very large applications.
- Read versus write, temporary storage versus persistent storage, consistency and locking, data sorting versus indexing, latency

### Integrating Azure Services with a Solution
- Azure Machine Learning: Cloud service that allow to create jobs to predictive do analytics. Examines large amounts of data to detect patterns, generate code to recognize those patterns.
- Big Data: HDInsight, uses Apache Hadoop (HortonWorks). Manage, Analyze and Report.
- Azure Search: PaaS service, integrated with REST API's and .NET SDK. Supports mulitple languages, simple query syntax, suggestions, highlight matches, facets and filters.

### Scalability and Performance of Azure Web Apps
- Globally Scale Azure Web Apps: CDN, Traffic Manager, Traffic Manager failover, Choosing the right database, Auto-Scale, Caching, Smart application architecture & design
- Develop Web Apps in .NET: Azure SDK for .NET
- Debugging Web Apps: Turn off customerrors in web.config, Publish debug version with symbols, Attach IDE to Azure server, Use server explorer, Enable remote debugging (disabled after 48 hours), Application logs, web server logs, detailed error logs, tracing logs.
- Language Options: .NET, Java, PHP, Ruby, NodeJS, Python, Powershell and other scripts.
- Difference Between Web Apps and VM and Cloud Services: Web Apps (PaaS, Package code and config, Autoscale, Multiple instances), Cloud Services (PaaS, VM based, Resizing causes downtime, remote desktop access, install software, Azure takes care of OS) and Virtual Machines (IaaS, do it yourself).

### Deploy Web Apps
- TBD

### Design for Business Continuity
- TBD

### Microsoft System Center for Hybrid Model
- TBD

### Monitoring
- TBD

### Business Continuity and Disaster Recovery
- TBD

### Azure Backup
- TBD

### Azure Automation
- Azure SDK for PowerShell, connect you azure account to PowerShell, PowerShell has more options than the portal, works with storage, vm's, etc.
- Workflows: runbooks, publish, running, scheduling, controlling VMs outside the VM

### Chef and Puppet
- Chef: open source, cloud and infra automation, available for Azure, AWS, Google Cloud, Powerful but complex, recipes called cookbooks
- Puppet: open source, cloud and infra automation, available for Azure, AWS, Google Cloud, VMWare, Powerful but complex, manifests and modules
- Desired State Configuration (DSC): forcing a desired state, ensures that the state remains in predefined consistent setting, e.g. check the security settings, e.g. check modules installed, e.g. avoid software to be installed.
- PowerShell can be used to enfore DSC. Azure Automation can turn those scripts into scheduled tasks that run in the cloud.

### New services
- Azure functions: small functions. (Bash, Batch, C#, F#, javascript, PHP, Powershell, Python). Consumption plan (per requests) or App Service Plan (uses VM's).
- Stream Analytics: For streaming data. Uses inputs (topics), queries (pattern matching) and outputs (subscribers)
- IoT Hub / Azure Events Hub: allows 2 way communication between many devices and the back-end. IoT Hub supports more protocols and supports 2 way communication. State management. Events Hub = one way and not state management.
- Service Fabric Cluster: Microservices platform. Microsofts' internal microservices platform. Supports state management, monitoring, fail-over, load balancing, etc. https://stackoverflow.com/questions/48415057/difference-between-kubernetes-and-service-fabric
- Azure Cloud Shell: Alternative to Powershell. Supports Bash environment and Powershell (windows) environment. Webbased interface.
- Azure Container Services (AKS): Kubernetes microservices platform. Managed by Azure. Developed by Google. Uses containers. Each VM has it's own operating system. Runs on a Host OS / Hypervisor. Containers virutalizes the application environment, allowing to move applications easily. Application lives inside the container. Containers are light weight. Quick, auto scaling, enables multi-cloud, provides auto-restart. Uses a manifest file (YAML - .yml). Similar to ARM templates.
- API Management for API Apps and Serverless Apps: API Gateway service. Has API Gateway features like API limits, caching, reporting, developer focussed portal and documentation, tokens, etc.
- Azure Key Vault: Manage cryptographic keys, also third party keys. Allows to no longer hard code the key inside the application. Has the option to use a hardware component.
- Virtual Machine Scale Sets (VMSS): Allows to deploy multiple virtual machines as a set. True autoscaling. Increases or decreases based on the performance (I/O or CPU) or fixed schedules. Limit of 1000 generic. 300 custom. Recommended to use placement groups (above 100 use singlePlacementGroup= false). Don't get public IP's by default. Use a load balancer and jump boxes to connect.
- Overview of Containers in Azure: AKS, Container instances (isolated containers, windows or linux, public ip, custom size), Container registry (store and manage docker images, works also with other container platforms), Service Fabric, App Service (deploy code directly from desktop to PaaS), Azure Batch (A service that allows large workloads to be deployed to).
- Network Watcher: Monitoring and diagnosis tool for your network. Topology (vm's, etc.). Package sniffer. Monitor network groups, Troubleshoot VPN problems. Troubleshoot VM connectivity issues. 1 network watcher per region.
- Data Lake Store: uses the HDFS standard to easy migration of Hadoop and Spark. Blobs have limites (500TB, file 195GB-8TB), Date Lake is optmized for throughput. Blobs can be replicated. Blocs can work with more languages.
- Storsimple: physical hardware device that is installed inside your on-prem network. Cloud appliance. Used for back-ups, archiving using secure channel. StorSimple Virtual Array is a virtual machine. 
- SQL Server Stretch DB: allows to scale SQL Server 2016 'cold data' into the Cloud. Uses your existing SQL Server instance. Good alternative to buying more local storage. Works on table level.
- Azure Database for PostgreSQL and MySQL: Fully managed PostgreSQL or MySQL. Has high availability. Auto backup and restore.
- Azure Monitor: Allows collection of metrics, activity logs and diagnostic logs. Can generate alerts and notifications based on all the resources. Is a more basic monitoring.
- Azure Log Analytics: Infrastructure monitoring tool for logging at infra level. Can analysis on-prem and cloud log files and stores the result central. Can connect to System Center Operations Manager (SCOM) or to a VM directly. Comparable to Splunk. 
- Azure Advisor: Azure Advisor is a tool that makes recommendations based on the usage and resources. High availability, security, performance and costs.
- Azure Data Catalog: Enterprise metadata catalog of all data sources. contains definitions, locations, tags and other information. Can be used to restrict access.

### Big Data
- HDInsight for ETL: Orchestration (Apache Oozie for scheduling, Azure Data Factory), Data Sources (Azure Blob Storage, Azure Data Lake Store, SQL Data Warehouse, Apache HBase, SQL Sources), Extraction (Apache Scoop for file transfer, Apache Flume for large amount of log data), Transform (SQL Server Integration Services, Split a single line of data into tables, validate against business rules), Hive for relational storage, Pig for processing, Pig works with SSIS.
- SQL Data Warehouse: Massively Parallel Processing (MPP), Data is broken into shards, Control node (the brain of the Database), Compute (computational power from 1 to 60 nodes), Data Movement Services - DMS coordinates data movements between all the nodes.
- Azure HDInsight Cluster Types: HDInsight = Apache Hortonworks Data Platform (HDP or Hadoop). 99.9% availabbility. Hadoop, Spark, Hive, LLAP, Hbase, Storm, etc. Works with HDFS (hadoop filesystem), Yarn (job scheduling) and MapReduce (parallel processing). Spark is an open source distributed compute engine. Hive is data warehouse for querying structured data. Works with HiveQL. Translates SQL to MapReduce. Hive LLAP is called interactive Query on Azure. HBase = column oriented key value store. Kafka to process streaming data, Storm for real-time analysis on streaming data.
- Azure Data Factory: Fully managed ETL service in the Cloud. Run SSIS packages in the Cloud. Piplelines (locical group of activities), activity (processing step), dataset (source of the data), linked services (input and output services). Azure Data Factory v2 is in preview.
