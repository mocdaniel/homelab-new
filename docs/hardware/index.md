---
icon: lucide/server
title: Hardware
description: This page contains an overview of the hardware in use in my homelab, grouped by primary purpose.
---

This page contains an overview of the hardware in use in my homelab, grouped by primary purpose.

## Compute

### Turing RK1 Compute Module

The [Turing RK1 Compute Module](https://docs.turingpi.com/docs/turing-rk1-specs-and-io-ports) is a Single Board Computer (SBC) that is approximately 5x more powerful than a Raspberry Pi CM4.

In my homelab, I am running 4 of them with identical specifications:

|Spec|Value|
|-|-|
|Instruction Set| ARMv8-A (64-bit)|
|CPUs|4x ARM Cortex-A76 + 4x ARM Cortex-A55|
|GPU|G610 GPU|
|NPU|6 TOPS|
|RAM|32GB LPDDR4|
|Storage|32GB eMMC 5.1|
|Ethernet|1Gbps|
|Power|5V/3A via USB Type-C|
|External Disk(s)|1TB NVMe M2 Samsung SSD 980|

#### turing-1

**192.168.1.11**{ .ip-badge .badge } **Kubernetes**{ .usage-badge .badge } **265€**{ .cost-badge .badge }

#### turing-2

**192.168.1.12**{ .ip-badge .badge } **Kubernetes**{ .usage-badge .badge } **265€**{ .cost-badge .badge }

#### turing-3

**192.168.1.13**{ .ip-badge .badge } **Kubernetes**{ .usage-badge .badge } **265€**{ .cost-badge .badge }

#### turing-4

**192.168.1.7**{ .ip-badge .badge } **Docker**{ .usage-badge .badge } **265€**{ .cost-badge .badge }
