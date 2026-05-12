# From Relational to Non-Relational Data Management
**Teacher** : Manel ZOGHLAMI \
**Moodle Link** : https://moodle.myefrei.fr/course/view.php?id=20435 \
**Grading** : 100% Project

-----
## Introduction to Cloud Computing
### Definition
**Cloud Computing** : "access computing resources over the Internet instead of owning and maintaining physical hardware locally"

### Traditional Computing *On-Premise* vs Cloud Computing
|    Traditional Computing    |             Cloud Computing            |
|-----------------------------|----------------------------------------|
| Org. buy physical servers   | Infrastructure is rented online        |
| Install software manually   | Resources can scale automatically      |
| Maintain data centers       | Maintenance is handled by the provider |
| Handle security and updates | Services are available globally        |
| Pay large upfront costs     | Users pay only for what they use       |

Cloud Computing reduces deployment time and operational complexity

### Introduction to Major Services
- **Amazon Web Services *AWS*** : Largest cloud provider
- **Microsoft Azure** : Strong integration with enterprise systems and Microsoft tools
- **Google Cloud Platform *GCP*** : Known for: AI, Big Data, Kubernetes

### Essential Characteristics
- **On-Demand Self-Service** : Users can provision resources automatically without human interaction with the provider
- **Broad Network Access** : Services are accessible over the network using standard devices
- **Resource Pooling** : Cloud providers share resources among multiple users using virtualization
- **Rapid Elasticity** : Resources can scale up or down quickly
- **Measured Service** : Cloud usage is monitored and billed according to consumption

### Types of Cloud Deployment Models
1. **Public Cloud**
    - Owned by a third-party provider
    - Advantages: Low initial cost, High scalability, Easy deployment
    - Disadvantage: Less control, Possible data privacy concerns

2. **Private Cloud**
    - Infrastructure is dedicated to a single organization, hosted internally, or by a third party
    - Advantages: Better control, Improved security, Custom configurations
    - Disadvantage: Higher cost, Requires management expertise

3. **Hybrid Cloud**
    - Combination of public and private clouds
    - Sensitive workloads remain private while scalable services use the public cloud

4. **Community Cloud**
    - Infrastructure shared by multiple organizations with similar requirements

### Types of Service Models
1. **Infrastructure as a Service *IaaS***
    - The provider offers: Virtual machines, Storage, Networking
    - The customer manages: Operating systems, Applications, Data
    - Advantages: High flexibility, Full control over systems
    - Disadvantage: Requires system administration skills

2. **Platform as a Service *PaaS***
    - The provider offers: Infrastructure, Operating systems, Runtime environments
    - The user focuses only on applications
    - Advantages: Faster development, Simplified deployment
    - Disadvantage: Less infrastructure control

3. **Software as a Service *SaaS***
    - Complete software delivered through the web
    - Users simply access the application
    - Advantages: No installation, Accessible everywhere, Automatic updates
    - Disadvantage: Limited customization, Internet dependency

### Cloud Computing, Virtualization & Big Data
Cloud computing relies heavily on virtualization and containerization technologies. These technologies allow efficient resource sharing, scalability, and rapid deployment.

Cloud computing is fundamental for Big Data because Big Data systems require Massive storage, Distributed processing, High scalability, Elastic computing power

### Advantages of Cloud Computing
- **Cost Reduction** : No need for expensive hardware investments
- **Scalability** : Resources adapt dynamically
- **High Availability** : Cloud providers offer redundant infrastructure
- **Global Access** : Applications can be accessed worldwide
- **Faster Deployment** : Infrastructure can be created within minutes
- **Backup and Disaster Recovery** : Many cloud providers include backup services

### Challenges and Risks of Cloud Computing
- **Security Concerns** : Data stored externally may raise privacy issues
- **Internet Dependency** : Cloud services require stable connectivity
- **Downtime Risks** : Even major cloud providers may experience outages
- **Vendor Lock-In** : Migrating between providers may be difficult
- **Compliance and Legal Issues** : Different countries have different regulations

### Summary
- Resources are delivered over the Internet
- Services are scalable and elastic
- Cloud reduces infrastructure management
- Different deployment and service models exist
- Cloud platforms support modern Big Data systems

-----
## Azure Global Infrastructure
Microsoft Azure is a **public cloud computing** platform developed by Microsoft. It provides a very large collection of online services that organizations can use without owning physical infrastructure.

### The Core Pillars of the Ecosystem
- **IaaS**: Virtual machines, storage, and networks. You manage the OS and software
- **PaaS** : Managed services for apps and databases. Azure handles the underlying infrastructure
- **SaaS** : Ready-to-use applications (like Microsoft 365) hosted in the cloud
- **Serverless** : Event-driven code execution (Azure Functions) where you only care about the logic, not the servers

### Data Centers
Azure’s infrastructure is designed to provide: High availability, Scalability, Fault tolerance, Low latency, Security and compliance, Worldwide service delivery

- **Data Centers** : physical facility that contains:
    - Servers
    - Storage systems
    - Networking equipment
    - Cooling systems
    - Power supplies
    - Security infrastructure

Azure data centers are highly secured and automated environments designed for continuous operation
- **Physical Security** : Microsoft uses multiple layers of security
- **Redundant Power Systems** : Backup generators, Multiple electrical feeds, Uninterruptible Power Supply
- **Cooling and Environmental Control** : Advanced cooling technologies to
maintain optimal operating temperatures and prevent hardware damage
- **Massive Scale** : A single Azure data center may contain: Hundreds of thousands of servers, Petabytes of storage, Extremely high-speed networks

### Regions
An Azure Region is a geographical area containing one or more Azure data centers connected through high-speed networks

Regions help organizations:
- Deploy services near users
- Reduce latency
- Meet legal requirements
- Improve availability
- Support disaster recovery

The chosen region affects:
- Performance
- Compliance
- Availability
- Pricing
- Disaster recovery strategy

Each Azure region operates independently. If one region experiences a failure, other regions can continue operating. This design is fundamental for **cloud resilience**

### Availability Zones
An Availability Zone (AZ) is a physically separate location inside an Azure region. Each zone has independent power, independent cooling, independent networking

AZ provides many benefits.
- **Fault Isolation** : A hardware or power failure in one zone does not affect the others.
- **High Availability** : Applications remain accessible even if part of the infrastructure fails.
- **Business Continuity** : Critical systems can continue running during infrastructure incidents

### Region Paris
A region pair consists of two regions within the same geographical area

- **Automatic Replication** : Some Azure services automatically replicate data to the paired region.
- **Planned Updates** : Microsoft generally avoids updating both paired regions simultaneously. This reduces the risk of simultaneous outages.
- **Disaster Recovery** : If an entire region becomes unavailable, services may fail over to the paired region
- **Geographic Separation** : Paired regions are geographically separated enough to reduce the risk of natural disasters, major power failures, network outages

### Edge Location
Edge locations are distributed network sites positioned closer to users

### Latency and Geographical Distribution
Latency is the delay between a request and the corresponding response, usually measured in milliseconds.

-----
## Big Data Storage/HDFS


-----
## Map-reduce and Big Data analytics


-----
## In-memory Processing- Apache Spark


-----
## Data streaming


-----
## NoSQL databases

