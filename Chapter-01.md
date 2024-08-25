# Chapter 1: The Start Point for Successful 5G

## Introduction

The telecommunications industry is at a pivotal moment, with significant business opportunities and technical challenges in building and delivering 5G services using hyperscaler infrastructures. Major communication service providers are working towards integrating their on-premise infrastructure with commoditized cloud computing to create scalable and accessible 5G solutions. Despite the unique approaches each provider takes, there is a pressing need for an open 5G solution blueprint that leverages common solution elements and open-source technologies, capable of working across multiple hyperscaler infrastructures.

## Why 5G with Cloud?

5G adoption rates vary across offerings such as Fixed Wireless Access (FWA) for consumers and businesses, edge deployments for latency-sensitive applications, and dedicated infrastructure for enterprises via network slicing. Expanding 5G coverage requires service providers to balance the significant financial burdens of capital expenditures (capex) and operational expenditures (opex). To meet diverse use cases with minimal capex and opex, an adaptable, on-demand, and pay-as-you-consume infrastructure is essential.

## 5G Solution Architecture

The 5G solution stack can be categorized into four main components: infrastructure, application platform, 5G applications, and management & orchestration. The infrastructure provides the necessary compute, network, and storage resources, while the application platform accommodates 5G applications with features like declarative state consistency, scaling, healing, and monitoring. The management and orchestration layer ensures dynamic scaling and efficient operation across multiple locations.

### Infrastructure

The infrastructure layer is composed of services and resources provided by cloud service providers. These include core services such as compute, network, storage, infrastructure sub-utilities (e.g., NTP source), additive network functions (e.g., firewalls, load balancers), and add-on software services such as identity management and infrastructure automation toolboxes. Despite the similarities among hyperscalers, the access methodologies, or APIs, vary, adding complexity to the management of different stacks. Application platform installers and management toolboxes can mitigate this complexity by introducing infrastructure agnosticism.

### Application Platform

The application platform is the core engine that runs the 5G application stack. Key components include container execution and orchestration platforms, application sub-utilities (dashboards, APIs, pluggable resources), and additive DevOps and platform-management toolboxes. This platform is not a singleton instance but a distributed, highly available, and resilient open-source software stack.

### 5G Applications

5G applications can be subcategorized into:

- **Core Network Functions (CNFs)**: These include essential network functions like the Access and Mobility Management Function (AMF), Session Management Function (SMF), and User Plane Function (UPF).
- **Supplementary Functions**: These include functions that enhance the capabilities of the core network, such as Network Exposure Function (NEF) and Network Slice Selection Function (NSSF).
- **Management Functions**: These involve the orchestration and management of the network, including functions like the Network Repository Function (NRF) and the Policy Control Function (PCF).

### Management & Orchestration

By the nature of communication solutions, the availability of 5G Core can be enhanced with multi-location deployment and location-aware access enablement to allow dynamic resource allocation and management. Multiple platform instances are required to host 5G application stacks, ensuring smooth and consistent platform creation, management, and application stack delivery. Leveraging the GitOps pattern, which uses Git as a single source of truth, is crucial for achieving homogeneous and scalable 5G Core across on-premise and hyperscaler environments.

## Case Studies and Real-World Applications

- **Case Study 1: Verizon Wireless**: Verizon Wireless utilized Kubernetes to modernize its core network functions. By containerizing these functions and deploying them on Kubernetes, Verizon achieved significant improvements in scalability and operational efficiency. The automation capabilities of Kubernetes allowed for streamlined operations, reducing the time required for network upgrades and maintenance.
- **Case Study 2: Deutsche Telekom**: Deutsche Telekom leveraged Kubernetes to build a flexible and scalable platform for its 5G network. The adoption of a microservices architecture and continuous integration/continuous deployment (CI/CD) practices enabled faster 5G rollout and improved agility in network operations.
- **Case Study 3: Rakuten Mobile**: Rakuten Mobile embraced Kubernetes to create a fully virtualized mobile network. The flexibility and cost-efficiency of Kubernetes allowed Rakuten to deploy network functions on commodity hardware, reducing capital expenditure and operational costs. The automation and orchestration capabilities enabled rapid deployment of new services and responsiveness to changing customer demands.

## Conclusion

The modernization of Telco applications using Kubernetes, service mesh, data mesh, OTel, and eBPF represents a strategic shift towards more agile, scalable, and efficient network operations. This chapter has laid the foundation for understanding the key components and benefits of this transformation. In the following chapters, we will delve deeper into specific technologies and their practical applications, showcasing real-world implementations and best practices.
