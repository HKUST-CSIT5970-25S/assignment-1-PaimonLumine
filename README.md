[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: FU, Xiaoyu
### Student Id: 20760670
### Email: xfuaj@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Phoronix Test Suite.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | Compre/Decompre | ------------------ |
    | ----------- | --------------- | ------------------ |
    | `t2.micro`  | 4036/3154 MIPS  |  11009.51 MB/S     |
    | `t2.medium` | 10150/5941 MIPS |  19283.68 MB/S     |
    | `c5d.large` | 7427/4871 MIPS  |  13787.26 MB/S     |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.
    > The performance does not scale linearly with the increase in vCPUs and memory resources since t2.medium's performance is better than c5d.large server.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 3210           | 0.320    |
    | `m5.large` - `m5.large`   | 4930           | 0.213    |
    | `c5n.large` - `c5n.large` | 4960           | 0.168    |
    | `t3.medium` - `c5n.large` | 2160           | 0.722    |
    | `m5.large` - `c5n.large`  | 2620           | 0.700    |
    | `m5.large` - `t3.medium`  | 4550           | 0.260    |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.
    > The network performance is better between instances of the same type than between instances of different types.
2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |  32.1          |  61.500  |
    | N. Virginia - N. Virginia |  4560          |  0.250   |
    | Oregon - Oregon           |  4950          |  0.190   |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
    > The network performance is better between instances deployed in the same region than between instances deployed in different regions.