# Chapter 3: Autoscaled 5G Core

## Introduction

Scalability is a fundamental aspect of the 5G technology stack. By leveraging Kubernetes constructs like replicasets and metrics-driven pod autoscaling, combined with multi-cluster management, we can achieve a scalable 5G Core implementation. Our testbed setup on a hyperscaler infrastructure validates the scalability design and architecture.

## Solution Architecture

The architecture includes a source repository for the 5G software stack, a management/hub cluster for cluster lifecycle management, and spoke/managed clusters for deploying 5G CNFs. We utilize Istio-based service mesh for observability and traffic steering, and a market-available toolbox for RAN and user plane emulation.

## TestBed Design & Verification

The testbed setup involves metrics collection through the Kubernetes metrics API and horizontal pod autoscaling (HPA) to match demand. By periodically adjusting the desired scale of the workload, the HPA ensures efficient resource utilization and scalability.

## Detailed Design Paradigms

1. **K8s Metrics Collection & Usage**:
   - Resource usage metrics, such as container CPU and memory usage, are available through the metrics API.
   - Metrics are used internally by Kubernetes capabilities like pod autoscaling and can be consumed externally for monitoring and analysis.

2. **HorizontalPodAutoscaler (HPA)**:
   - Automatically updates workload resources to match demand by scaling the number of pods horizontally.
   - The HPA controller adjusts the desired scale based on observed metrics like CPU and memory utilization.

3. **Vertical Pod Autoscaler (VPA)**:
   - Adjusts resource limits and requests for containers in pods based on usage.
   - Helps maintain appropriate resource allocation for each pod, ensuring efficient scheduling and resource utilization.

4. **Cluster Autoscaler (CA)**:
   - Adjusts the size of the Kubernetes cluster to meet current needs.
   - Increases cluster size when there are pods that cannot be scheduled due to insufficient resources and decreases size when nodes are underutilized.

## Challenges & Solutions

1. **HPA vs. VPA for 5G Stack**:
   - While HPA scales the number of pods, VPA adjusts resource allocation for existing pods. For 5G core, HPA is preferred to avoid service outages caused by pod restarts.

2. **Cluster Scaling for 5G Workloads**:
   - Cluster Autoscaler works in conjunction with HPA to ensure that new pods have the necessary resources by scaling the cluster size as needed.

3. **Smart Workload Scheduling**:
   - Leveraging GitOps for consistent workload deployment and configuration management across clusters.
   - Ensuring no service degradation during scaling by implementing policies for critical CNFs.

## Implementation Case Study: Autoscaling in Action

In our implementation, we used the open5gs project for the 5G software stack, deployed on a hyperscaler infrastructure. By leveraging Kubernetes autoscaling features, we achieved seamless scalability for 5G core functions, ensuring efficient resource utilization and high availability. The testbed demonstrated the effectiveness of HPA and CA in managing dynamic traffic loads and maintaining service quality.

## Conclusion

The autoscaling capabilities of Kubernetes, combined with multi-cluster management, provide a robust framework for deploying scalable 5G core networks. This chapter has detailed the architecture, design paradigms, and practical implementation of autoscaling in a 5G environment. In the next chapter, we will explore the role of service mesh in enhancing connectivity and managing microservices communications within Telco networks.