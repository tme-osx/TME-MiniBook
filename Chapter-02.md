# Chapter 2: Distributed Scalable 5G with Observability

## Abstract

Telecommunication, Media, and Entertainment (TME) solutions are designed for high availability, accuracy, low latency, and regulatory compliance. These solutions traditionally include operational support systems (OSS) and business support systems (BSS) to monitor and manage network performance and business workflows. The complexity of modern 5G Core platforms, combined with the need for scalability and efficient traffic management, necessitates advanced observability and traffic steering solutions.

## Introduction

The deployment of 5G networks represents a significant leap in telecommunications, introducing complex distributed systems that must manage vast amounts of data across multiple locations with minimal latency. Ensuring the performance, reliability, and security of these networks requires robust observability frameworks that can provide real-time insights into every component of the infrastructure.

In traditional hyperscaler infrastructure, regions are divided into availability zones with distributed compute, network, and storage services. However, variations in availability and cost among hyperscalers can limit workload portability. To address this, we base our solution blueprint on infrastructure-agnostic platform components such as Red Hat OpenShift, Red Hat Advanced Cluster Management, and Red Hat OpenShift Service Mesh.

## The Challenge of Observability in Distributed 5G Networks

In a distributed 5G network, observability is more than just monitoring. It encompasses the ability to trace, log, and measure the performance of every microservice and network function across multiple clusters and geographic locations. The complexity of 5G networks, with their diverse components and high-speed data flows, makes it essential to deploy an observability strategy that can scale with the network and provide actionable insights.

## Enhanced Observability Section

### Infrastructure-Level Observability

#### Compute: Project Kepler

**Project Kepler** is a vital tool for monitoring and optimizing energy consumption in cloud-native environments. In a 5G setting, where efficient resource utilization is crucial, Kepler provides valuable insights into the power usage of workloads running on Kubernetes clusters.

- **Metrics Collection**: Kepler gathers data on CPU, memory, and power consumption, helping operators to fine-tune the energy efficiency of their infrastructure without compromising on performance.
- **Integration**: Kepler seamlessly integrates with Kubernetes and can work alongside observability tools like Prometheus for comprehensive monitoring and Grafana for visualization, enabling telecom operators to maintain optimal performance while reducing energy costs.

#### Network: NetObserv Operator

**NetObserv Operator** is designed to enhance network observability within Kubernetes environments. It provides deep visibility into network traffic, which is essential for maintaining the high-performance requirements of 5G networks.

- **Traffic Monitoring**: NetObserv collects and analyzes network traffic data, providing insights into packet flows, latency, and throughput across different segments of the 5G network.
- **Security and Compliance**: By monitoring network traffic in real-time, NetObserv can detect anomalies and potential security threats, enabling operators to respond proactively to protect their infrastructure.
- **Integration with Service Mesh**: NetObserv can be used in conjunction with service mesh solutions to provide end-to-end visibility into service-to-service communication, making it easier to diagnose and resolve network-related issues.

#### Storage: Persistent Storage Observability

In 5G networks, storage observability is crucial for ensuring data availability and integrity across distributed environments. Observability tools can monitor the performance of storage systems, track latency, and identify bottlenecks that could impact the overall network performance.

- **Monitoring Tools**: Tools like Prometheus and Grafana can be used to monitor the performance of persistent storage systems, providing metrics on I/O operations, latency, and error rates.
- **Integration with Kubernetes**: Kubernetes-native storage solutions, such as OpenEBS, provide additional observability features, including metrics collection and visualization, helping operators ensure that their storage systems are operating efficiently and reliably.

### Software Stack Observability

#### Application Layer: CNF/NFV Observability

In the application layer, observability focuses on monitoring the performance and reliability of Containerized Network Functions (CNFs) and Network Function Virtualization (NFV) components. These functions are critical to the operation of 5G networks and require continuous monitoring to ensure they are meeting performance and latency requirements.

- **Custom Metrics with OpenTelemetry (OTel)**: OTel allows operators to instrument CNFs and NFVs with custom metrics, enabling detailed monitoring of specific functions like packet processing rates, session establishment times, and error rates.
- **End-to-End Tracing**: OTel’s tracing capabilities provide insights into the entire lifecycle of a network request, from the initial connection to the final data packet delivery, helping to identify bottlenecks and optimize performance.

#### Platform Layer: Kubernetes Observability

Kubernetes is the backbone of modern cloud-native 5G networks, and its observability is critical for maintaining the health and performance of the network.

- **Kubernetes Metrics**: Metrics Server, Prometheus, and Grafana are commonly used to monitor Kubernetes clusters, collecting data on CPU usage, memory consumption, pod health, and more.
- **Cluster-Level Observability**: Tools like Red Hat Advanced Cluster Management provide a holistic view of multi-cluster environments, enabling operators to monitor and manage Kubernetes clusters across different geographic locations from a single interface.
- **Security Monitoring with eBPF**: eBPF enhances Kubernetes observability by providing deep visibility into kernel-level operations, allowing operators to monitor system calls, network traffic, and application behavior in real-time.

#### Operating System Layer: Linux Observability

At the operating system level, observability focuses on monitoring Linux-based systems, including both user space and kernel space. This is essential for understanding the performance and behavior of the underlying infrastructure that supports 5G networks.

- **System Performance Monitoring**: Tools like BPFTrace, built on top of eBPF, allow operators to trace and monitor system calls, network operations, and file system activity, providing insights into potential performance issues or security threats.
- **Bare Metal Observability**: In environments where 5G functions run on bare metal servers, monitoring tools like Redfish and IPMI provide critical data on hardware health, BIOS settings, and system logs. These tools help ensure that the physical infrastructure is operating optimally and securely.

### Single Pane of Truth Approach

To manage the complexity of observability across different layers of the infrastructure and software stack, a single pane of truth approach is essential. This approach involves aggregating data from various observability tools into a unified dashboard, providing operators with a comprehensive view of the network’s health and performance.

- **Unified Dashboards**: Platforms like Grafana can be configured to pull data from multiple sources, including Prometheus, OTel, and eBPF, presenting it in a cohesive dashboard that covers all aspects of the network.
- **Advanced Cluster Security**: Integrating security observability into the single pane of truth approach ensures that operators have visibility into potential threats at every layer of the stack, from the application to the infrastructure level.
- **Automated Alerts and Response**: By consolidating observability data into a single platform, operators can set up automated alerts for specific metrics or anomalies, enabling faster response times to incidents and reducing the risk of service disruptions.

## Solution Overview

3GPP standards envision a distributed 5G core with user plane function (UPF) placement based on user location. Our testbed setup includes a central SMF accessing multiple UPFs across different clusters and locations. This setup ensures that the right UPF instance is selected based on variables like DNN, TAC, and cell ID.

The integration of Kubernetes, service mesh, and advanced observability tools like OpenTelemetry (OTel) and eBPF provides a powerful solution for managing and observing distributed 5G networks. These technologies enable operators to scale network functions dynamically, manage traffic efficiently, and gain deep visibility into network performance and security.

## The Role of Kubernetes in Distributed 5G Networks

Kubernetes plays a critical role in managing the distributed nature of 5G networks. Its inherent capabilities for container orchestration, scaling, and self-healing make it an ideal platform for deploying and managing 5G Core network functions. Key advantages include:

- **Multi-Cluster Management**: Kubernetes supports the deployment and management of network functions across multiple clusters, which is essential for ensuring that 5G services can be delivered with low latency and high availability across different regions.
- **Dynamic Scaling**: Kubernetes' Horizontal Pod Autoscaler (HPA) and Cluster Autoscaler (CA) features allow 5G network functions to scale automatically based on real-time demand, ensuring that resources are allocated efficiently without manual intervention.

## Service Mesh Federation

Service mesh federation allows sharing services and workloads between separate meshes managed in distinct administrative domains. This approach ensures that communication between meshes is explicitly opt-in, aligning with the principle of least privilege. Our implementation involves configuring ingress and egress gateways for each service mesh, specifying trust domains, and declaring exported and imported services for federation.

In a 5G environment, service mesh plays a crucial role in managing the complex communication patterns between microservices. By integrating service mesh with 5G network functions, operators can:

- **Control Traffic Flows**: Service mesh enables fine-grained control over how traffic is routed between network functions, allowing for advanced traffic management strategies that can optimize performance and reduce latency.
- **Enhance Security**: Service mesh provides built-in security features such as mutual TLS, ensuring secure communication between network functions without requiring modifications to the application code.
- **Improve Observability**: Service mesh provides detailed metrics, logs, and traces that give operators deep insights into the performance and behavior of the network functions.

## Observability with Submariner and L7 Mesh Connectivity

Submariner enables direct networking between Pods and Services across Kubernetes clusters, simplifying network configuration and enhancing observability. Additionally, advanced observability solutions like NetObserv Operator and Red Hat Advanced Cluster Security provide centralized monitoring and actionable insights for multi-cluster 5G deployments.

OpenTelemetry (OTel) and eBPF are instrumental in building an observability framework that can meet the demands of distributed 5G networks. By leveraging these tools, operators can achieve:

- **End-to-End Tracing**: OTel provides end-to-end tracing capabilities that allow operators to monitor the flow of data through the 5G Core, from the AMF to the UPF, and detect bottlenecks or performance issues in real-time.
- **Real-Time Metrics**: OTel collects metrics on the performance of individual microservices and network functions, providing real-time visibility into CPU usage, memory consumption, network throughput, and error rates.
- **Deep System Insights with eBPF**: eBPF enables high-performance monitoring and tracing within the Linux kernel, offering deep visibility into system calls, network traffic, and application behavior. This is particularly valuable for detecting security threats and optimizing the performance of critical network functions.

## Implementation Details

- **Service Mesh Peering Architecture for 5G**: Involves configuring the ServiceMeshControlPlane on each service mesh to create ingress and egress gateways, specifying trust domains, and declaring exported and imported services for federation. This architecture supports seamless integration and communication between multiple service meshes, ensuring efficient management of 5G core functions across distributed locations.

- **Network Observability and Management**: Leveraging tools like Submariner and NetObserv Operator enables real-time monitoring and management of network traffic across different clusters. This setup provides visibility into traffic patterns, performance metrics, and potential issues, allowing for proactive management and optimization of network resources.

## Challenges and Solutions

### Scalability

Ensuring that the 5G core can scale efficiently across multiple locations requires robust automation and management tools. By integrating solutions like Red Hat Advanced Cluster Management and leveraging GitOps practices, operators can achieve consistent and scalable deployments.

### Security

Protecting network traffic and ensuring secure communication between distributed components is critical. Implementing security measures such as encryption, access controls, and continuous monitoring helps safeguard the network.

### Performance Optimization

Achieving optimal performance in a distributed 5G core involves balancing load across different clusters and minimizing latency. Techniques such as traffic steering, load balancing, and intelligent routing are essential for maintaining high performance.

## Case Study: Implementation at a Major Telecom Provider

A major telecom provider implemented a distributed 5G core using the described architecture. By leveraging service mesh federation and Submariner for network connectivity, the provider achieved seamless integration and efficient management of 5G core functions across multiple locations. The implementation resulted in improved scalability, enhanced observability, and optimized performance, ensuring a high-quality user experience.

## Conclusion

The integration of advanced observability and traffic management solutions is essential for the successful deployment and operation of distributed 5G core networks. By leveraging technologies like service mesh federation, Submariner, NetObserv Operator, and OpenTelemetry, telecom operators can achieve efficient management, enhanced security, and optimized performance in their 5G deployments. This chapter has provided an in-depth look at the architecture, implementation details, and real-world applications of these technologies, setting the stage for further exploration in subsequent chapters.
