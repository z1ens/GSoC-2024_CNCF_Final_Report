
# Google Summer of Code (GSoC) 2024 Final Report

**Contributor:** [Zhe Shen](https://github.com/z1ens)  
**Organization:** [Cloud Native Computing Foundation (CNCF)](https://www.cncf.io)  && [Open-Cluster-management](https://open-cluster-management.io)  
**Project:** [[GSoC 2024]Scheduling AI Workload Among Multiple Clusters](https://github.com/open-cluster-management-io/ocm/issues/369)

## Background

[Open Cluster Management (OCM)](https://open-cluster-management.io) is a [CNCF](https://www.cncf.io) project focused on Multi-Cluster and Multi-Cloud management for Kubernetes applications. It offers open APIs for cluster registration, workload distribution, and dynamic placement of policies and workloads. The placement concept in OCM enables developers to deploy workloads dynamically across clusters based on resource availability, such as memory and CPU.

### Project Overview

This project enhances OCM to optimize AI workload scheduling across multiple Kubernetes clusters by focusing on GPU/TPU resource utilization. 

The key components include:

1. GPU/TPU Resource Evaluation Addon:
- Extends OCM’s `Placement` strategy by extending `AddonPlacementScore` to evaluate GPU/TPU resources within cluster sets. This informs scheduling decisions to ensure AI workloads are effectively distributed according to specific GPU/TPU resource requirements.

2. OCM Kueue Admission Check Controller:
- Deliver a proposal for the external Kueue Admission Check controller integrating OCM Placement results with MultiKueue. The controller reads OCM Placement decisions and generates corresponding MultiKueueConfig and MultiKueueCluster resources, streamlining the setup of the MultiKueue environment and enabling users to select clusters based on custom criteria. 


These components aim to significantly improve the scheduling of AI workloads, ensuring they are efficiently dispatched based on the availability of specialized resources like GPUs and TPUs.

## Work Completed

### Deliverables

- GPU/TPU Resource-Usage-Collect-Addon 
- Proposal of the OCM Kueue Admission Check Controller
- Demonstrate both of my work in the OCM community meeting.

## Roadmap
### Phase 1: Understanding and Enhancing Resource Usage Collection

- **Environment Setup**:
  - Set up a local Kubernetes (Kind) cluster that can run GPU pods.
  - Ensure the cluster is configured to expose the information of the `gpu-node`.

- **Install OCM**: 
  - Set up the Open-Cluster-Management (OCM) environment.

- **Learn OCM Architecture**: 
  - Deep dive into the architecture of OCM, focusing on:
    - The "hub-kubelet" mode.
    - The concept of `Placement`.
    - The workflow of `Addon` components.
    - The enhancement in using `AddonTemplate`.

- **Study AddOnPlacementScore**: 
  - Understand the `AddOnPlacementScore` API and how it integrates with OCM's scheduling mechanism.

- **Analyze Existing Resource Usage Collect Addon**:
  - Review the workflow and scoring mechanism of the current resource usage collect addon.
  - Explore the existing method for resource collection and scoring.

- **Extend to GPU and TPU Resource Collection**:
  - Research and implement methods to collect GPU and TPU resource usage.
  - Develop and integrate scoring mechanisms for these resources.

- **Develop Addon with `AddonTemplate` Mode**:
  - Refactor the addon using the new `AddonTemplate` mode to enhance code cleanliness and maintainability.
  - Ensure the new template structure aligns with best practices and OCM's extensibility features.

- **Develop New Scoring Mechanisms**:
  - Implement a **Node Scope Score** to evaluate resources at the node level.
  - Implement a **Cluster Scope Score** to ensure resources are efficiently and reasonably scheduled across clusters.

- **Community Engagement**:
  - Present my progress and contributions in OCM community meetings.
  - Demonstrate the enhanced resource usage collect addon with GPU/TPU support.

## Phase 2: Integrating MultiKueue and Kueue

- **Set Up MultiKueue Environment**:
  - Prepare and configure a MultiKueue environment.

- **Research Kueue and MultiKueue Mechanisms**:
  - Study the workflow and internal mechanisms of Kueue and MultiKueue.
  - Understand their interaction with job scheduling and resource allocation.

- **Proposal Development**:
  - Draft and deliver a proposal for an OCM Kueue Admission Check Controller.

- **Integrate OCM with MultiKueue**:
  - Integrate the OCM placement results with MultiKueue.
  - Utilize the `AddOnPlacementScore` from the resource usage collect addon to dynamically adjust job dispatching in MultiKueue.

- **Final Demonstration**:
  - Showcase the integrated solution and its effectiveness in an OCM community meeting.

## Current State
- Node Scope and Cluster Scope scoring mechanisms are integrated and operational within the OCM framework.
- The addon successfully contributes scores that influence workload placement decisions.

## Future Work
- Further refinement of the Kueue Admission Check controller.
- Expanding support for more complex scheduling scenarios and additional resource types.

## Challenges & Learnings
- Balancing between bin-packing and spreading strategies required careful consideration of different use cases.
- Gained significant experience in Kubernetes scheduling and Golang development.

## Code Contributions
- Merged resource scoring mechanisms and addon into the [addon-contrib repository](https://github.com/open-cluster-management-io/addon-contrib).



