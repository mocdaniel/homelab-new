---
icon: lucide/drafting-compass
title: Architecture
description: This page contains information on the architecture of the Kubernetes environment in my homelab.
---

This page contains information on the architecture and capabilities of the Kubernetes environment in my homelab. Below you can find introductory information on various aspects of the environment, with links leading you to more detailed information in the respective sections of this documentation.

## Cluster Resources

The cluster runs on four [Turing RK1 compute modules](../hardware/index.md), thus resulting in the following combined resources being available in the cluster:

|Resource|Value|
|-|-|
|CPUs|32 Cores|
|RAM|128GB|
|Disk|4TB SSD storage|

## Operating System

The OS of choice for my Kubernetes environment is [Talos](https://talos.dev). The reasons for this are simple:

- Immutable
- Declarative
- Minimal
- Support for [my hardware](../hardware/index.md#turing-rk1-compute-module)

You can find more information on Talos [here](./talos.md).

## Operating Mode

Kubernetes is configured in **High Availability mode**, with 3 nodes being members of the control plane. This ensures that even in case of node updates or failures, the cluster API continues to work:

- **Control plane nodes**: `talos-1`, `talos-2`, `talos-3`
- **Worker nodes**: tba

Since the cluster consists of just 4 nodes in total, the control plane nodes are configured to allow for 'normal' workloads to be scheduled on them. This means that the total cluster load is (roughly) equally shared among all four nodes, despite just one of them being a worker node.

## Networking

My Container Network Interface (CNI) of choice is [Cilium](https://cilium.io). It has been adopted by most cloud providers and many end users as the de-facto default CNI for Kubernetes, and comes with a lot of features useful for my homelab, e.g.

- support for cluster-wide and node-level `NetworkPolicies`
- L2 load balancing
- doesn't need kube-proxy

You can find more information on Cilium [here](./cilium.md).

## Storage

As outlined in the [Hardware](../hardware/index.md#turing-rk1-compute-module) section, all cluster nodes posses very little disk space (just 32GB), but are equipped with 1TB NVMe SSDs. Therefore, the Kubernetes clusters makes almost no use of local disk storage, and instead utilizes `PersistentVolumes` for persistent data.

The storage engine used in the cluster is [Rook](https://rook.io), which provides file-, block-, and object storage on Kubernetes based on Ceph.

You can find more information on Rook [here](./rook.md).

## Deployments

The Kubernetes components running in the cluster need to be deployed somehow. This includes _infrastructure_ workloads such as Cilium or Rook, as well as applications I am self-hosting within the cluster.

These applications are installed and managed using a _GitOps_ approach. The GitOps engine in question is [Flux](https://fluxcd.io). I went with Flux because it's lightweight and provides full OCI support.

You can find more information on Flux [here](./flux.md).


## Observability

Observing all the moving parts of a Kubernetes cluster can quickly become overwhelming. Goal number 1 for me was not to reinvent the wheel.

Since I am using [Grafana Cloud's](https://grafana.com/products/cloud/?plcmt=products-nav) freemium tier, I am leveraging many of the available integrations for Kubernetes, Docker, etc. using **Alloy**, Grafana's OTel collector distribution.

This also allows me to manage a fleet of Alloy instances, should I require multiple OTel collectors in the future. 

You can find more information on observability of my homelab [here](../observability/index.md).
