
# Google Summer of Code (GSoC) 2024 Final Report

**Contributor:** [Zhe Shen](https://github.com/z1ens)  
**Organization:** [Cloud Native Computing Foundation (CNCF)](https://www.cncf.io)  && [Open-Cluster-management](https://open-cluster-management.io)  
**Project:** [[GSoC 2024]Scheduling AI Workload Among Multiple Clusters](https://github.com/open-cluster-management-io/ocm/issues/369)

## TL;DR

This is my first time participating in Google Summer of Code. And I have successfully completed the project, including the development of an addon and the Kueue admission check controller.
- **Key Links**:
  - [Community Demo (Addon)](link to the community meeting)
  - [OCM Repository (Kueue Controller Proposal)](link to the repository)

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

### Phase 2: Integrating MultiKueue and Kueue

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

### Addon Development

- **Pull Request Status**: There is an ongoing [Pull Request](https://github.com/open-cluster-management-io/addon-contrib/pull/20) for the `Addon` section, which is currently under code review. While the review process is still in progress, all core functionalities have been implemented.

- **Community Demo**: The `Addon` has already been demonstrated in a community demo, and the recording is available on YouTube [here](https://www.youtube.com/watch?v=b9h-uwZw7jA&t=310s).

REF: 
- [GPU/TPU-resource-usage-collect-addon #20](https://github.com/open-cluster-management-io/addon-contrib/pull/20)
- [Open Cluster Management - AI Workload Scheduling Addon + ArgoCD Pull Integration v2 POC](https://www.youtube.com/watch?v=b9h-uwZw7jA&t=310s)

### Kueue Admission Check Controller

- **Proposal Review**: The proposal for the Kueue admission check controller has undergone an initial review.

- **Community Presentation**: This proposal was also presented during the OCM community meeting, receiving feedback for further refinement.

- **Next Steps**: We plan to further improve the proposal based on the feedback and review before merging it into a specific OCM repository [here](https://github.com/open-cluster-management-io/ocm/tree/main/solutions).

REF: [OCM Kueue Admission Check Controller Proposal](https://github.com/z1ens/OCM_Kueue_Admission_Check_Controller/blob/main/README.md)

## Future Work

- **Addon Code Refinement**: Focus will be placed on refining the current addon code to incorporate community feedback and to address additional use cases. Once all relevant issues are resolved and discussions are concluded, the addon will be merged into the [addon-contrib repository](https://github.com/open-cluster-management-io/addon-contrib) for ongoing maintenance and improvement.

- **Kueue Controller Integration**: The Kueue admission check controller will be merged into the [designated OCM repository](https://github.com/open-cluster-management-io/ocm/tree/main/solutions) after thorough review.

## Challenges & Learnings

### Mentorship and Guidance
- **Role of Mentors**: I am immensely grateful to my mentors, Qing Hao and Jian Qiu. Particularly Qing Hao, who has been instrumental in guiding me through every detail of this project. Her support has been not just technical but also emotional, offering congratulations after successful demos and reassurance during challenges.

### Problem-Solving Approach

- **Initial Struggles**: Early in my GSoC journey, I often tried to solve issues independently, leading to frustration and I found out that I was always stuck somewhere.

- **Learning to Collaborate**: I realized the value of consulting my mentors and discussing problems with the community, which often led to quick resolutions. This experience taught me the importance of seeking guidance from experts and engaging more with the community.

### Growth Through Challenges

- **Embracing Failure**: I learned that failure is a part of growth. During a recent demo, I faced a minor issue that initially made me very nervous. However, my mentors and the host reassured me, which helped me see that mistakes are opportunities to learn, not failures.

- **Developing Composure**: This experience also highlighted the importance of maintaining composure during important presentations. I learned to stay calm, present my points clearly, and then return to address any issues.
