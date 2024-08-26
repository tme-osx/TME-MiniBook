# Chapter 3: Autoscaled 5G Core

## Introduction

Scalability is a fundamental aspect of the 5G technology stack. By leveraging Kubernetes constructs like replicasets and metrics-driven pod autoscaling, combined with multi-cluster management, we can achieve a scalable 5G Core implementation. Our testbed setup on a hyperscaler infrastructure validates the scalability design and architecture. In this chapter, we delve into the intricacies of scaling 5G networks and provide real-world examples of how autoscaling has been implemented successfully in the telecom industry.

## Understanding Autoscaling in Kubernetes

Kubernetes provides robust tools for managing the scalability of containerized applications, which are essential for the dynamic demands of a 5G Core. Autoscaling in Kubernetes can be broadly categorized into three types:

1. **Horizontal Pod Autoscaler (HPA)**: Scales the number of pod replicas in a deployment or replica set based on observed CPU utilization, memory usage, or custom metrics.
2. **Vertical Pod Autoscaler (VPA)**: Adjusts the resource limits and requests for individual containers in a pod based on their actual usage.
3. **Cluster Autoscaler (CA)**: Adjusts the number of nodes in a cluster based on the pending pod's resource requests that cannot be met by the current cluster size.

Each of these autoscaling mechanisms plays a critical role in maintaining the performance and reliability of 5G Core functions under varying traffic loads.

## Solution Architecture

The architecture of an autoscaled 5G Core involves several key components:

- **Source Repository**: Houses the 5G software stack, including core network functions (CNFs) and supplementary services.
- **Management/Hub Cluster**: Manages the lifecycle of clusters, including updates, scaling, and policy enforcement.
- **Spoke/Managed Clusters**: Deploy 5G CNFs and handle the traffic and workloads specific to different geographic locations or network slices.
- **Service Mesh**: Provides observability, traffic steering, and security across the distributed microservices architecture.

In our testbed, we validated this architecture on a hyperscaler infrastructure, ensuring that the design could scale dynamically in response to real-time network demands.

## Real-World Example: Autoscaling at Rakuten Mobile

**Background**: Rakuten Mobile, a Japanese telecom operator, built the world's first fully virtualized mobile network using a cloud-native approach. One of the critical challenges they faced was ensuring that their 5G Core could scale efficiently to meet fluctuating user demands while maintaining high performance and reliability.

**Implementation**:
- **Horizontal Scaling**: Rakuten Mobile utilized Kubernetes' HPA to scale its 5G Core network functions based on real-time traffic patterns. For instance, the User Plane Function (UPF) instances were scaled up during peak hours when data traffic surged and scaled down during off-peak times to optimize resource utilization.
- **Vertical Scaling**: They implemented VPA to automatically adjust the CPU and memory limits of their CNFs, ensuring that each network function had the necessary resources to operate efficiently without over-provisioning.
- **Cluster Autoscaling**: To manage the infrastructure costs, Rakuten Mobile used Cluster Autoscaler to dynamically add or remove nodes in their Kubernetes clusters based on the workload demands, particularly during special events like large-scale sports events where traffic spikes were expected.

**Outcome**: Rakuten Mobile successfully maintained high network performance and availability while optimizing their resource usage. The autoscaling mechanisms reduced operational costs by eliminating the need for manual intervention and allowing the network to adapt to varying traffic conditions automatically.

## Detailed Design Paradigms

1. **K8s Metrics Collection & Usage**:
   - Kubernetes uses the Metrics Server to collect resource usage data such as CPU and memory utilization from the kubelets. This data is critical for making autoscaling decisions.
   - In a 5G network, metrics like packet processing rates, session establishment times, and latency are also collected and used to trigger scaling actions.

2. **Horizontal Pod Autoscaler (HPA)**:
   - HPA is configured to scale the number of pods based on the CPU utilization of the 5G Core functions. For example, if the CPU usage of the UPF pods exceeds a certain threshold, HPA automatically increases the number of UPF pods to handle the additional load.
   - Custom metrics, such as the number of active sessions or the volume of traffic, can also be used to drive HPA decisions, making the scaling more responsive to network-specific demands.

3. **Vertical Pod Autoscaler (VPA)**:
   - VPA is used to adjust the CPU and memory requests of pods in real-time based on their current usage. For instance, during a traffic surge, VPA can increase the resource limits of the AMF pods to ensure they can handle the increased signaling load.
   - This dynamic adjustment prevents resource over-provisioning and ensures that each network function has the optimal amount of resources to operate efficiently.

4. **Cluster Autoscaler (CA)**:
   - Cluster Autoscaler works in conjunction with HPA and VPA to ensure that there are enough nodes in the cluster to accommodate the scaled-up pods. If the current cluster size is insufficient to meet the demands of a new workload, CA automatically provisions additional nodes.
   - Conversely, when the workload decreases, CA can reduce the number of nodes, ensuring that the cluster operates cost-effectively without sacrificing performance.

## Challenges & Solutions

1. **HPA vs. VPA for 5G Stack**:
   - While HPA scales the number of pods, VPA adjusts resource allocation for existing pods. For 5G core, HPA is preferred to avoid service outages caused by pod restarts. However, a combination of HPA and VPA can be used to ensure both scalability and optimal resource utilization.
   - For example, in scenarios where session loads are highly variable, HPA can handle scaling the number of session management pods, while VPA ensures that each pod is equipped with the necessary resources to manage the sessions effectively.

2. **Cluster Scaling for 5G Workloads**:
   - Cluster Autoscaler works in conjunction with HPA to ensure that new pods have the necessary resources by scaling the cluster size as needed. This is particularly important in multi-cluster deployments where traffic loads can vary significantly across regions.
   - In a real-world scenario, a telecom operator might use Cluster Autoscaler to add more nodes in a specific geographic region during a major event, such as a concert or sports event, where a sudden spike in data traffic is expected.

3. **Smart Workload Scheduling**:
   - Leveraging GitOps for consistent workload deployment and configuration management across clusters. GitOps ensures that all changes to the network configuration are version-controlled and automatically applied across all clusters, reducing the risk of configuration drift.
   - To avoid service degradation during scaling, policies for critical CNFs can be implemented. For example, traffic can be temporarily rerouted to other pods or clusters during scaling operations to ensure continuous service availability.

## Implementation Case Study: Autoscaling in Action

**Background**: A major European telecom operator needed to ensure their 5G Core could handle the fluctuating demands of millions of users across multiple countries. They sought to implement an autoscaling solution that could dynamically adjust to these demands while minimizing operational costs.

**Implementation**:
- The operator used Kubernetes HPA to scale their 5G Core network functions, including the Access and Mobility Management Function (AMF) and Session Management Function (SMF), based on real-time CPU and memory usage.
- VPA was deployed to adjust the resource limits for the User Plane Function (UPF) based on actual traffic demands. This ensured that each UPF pod had enough resources to process user data without over-allocating resources during low-traffic periods.
- Cluster Autoscaler was integrated to manage the infrastructure costs by adding and removing nodes in the Kubernetes clusters based on the real-time requirements of the network.

**Outcome**: The telecom operator achieved seamless scalability for their 5G core functions, ensuring efficient resource utilization and high availability. The autoscaling mechanisms allowed the network to handle peak traffic periods without manual intervention, reducing operational costs and improving service quality.

## Conclusion

The autoscaling capabilities of Kubernetes, combined with multi-cluster management and advanced observability tools, provide a robust framework for deploying scalable 5G core networks. Real-world implementations, such as those at Rakuten Mobile and other leading telecom operators, demonstrate the effectiveness of these technologies in managing the dynamic demands of 5G networks. This chapter has detailed the architecture, design paradigms, and practical implementation of autoscaling in a 5G environment. In the next chapter, we will explore the role of service mesh in enhancing connectivity and managing microservices communications within Telco networks.
