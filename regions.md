# Regions

## General
- Cluster of data centers
- Most AWS services are region-scoped
- Utilizing a service in another region will be another "instance"

## How to choose a region?
- Compliance: sometimes there are legal requirements where data can never leave a region without explicit permission
- Availability: not all services and features are available in every region
- Pricing: varies between regions
- Proximity: reduced latency when server is in closer proximity to customers

## [Availability Zones (AZ)](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/use-fault-isolation-to-protect-your-workload.html)
- 1+ discrete data centers with redundant power, networking, and connectivity
- Fault isolated (limits effect of failure)
- Linked together with high bandwidth, ultra-low latency networking
- Region is formed with usually 3, min 2, max 6 AZs

<img src="./images/region-azs.png" alt="availability zones" width="400" />
