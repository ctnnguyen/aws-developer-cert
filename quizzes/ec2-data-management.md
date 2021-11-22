# EC2 Data Management

1). You have just terminated an EC2 instance in `us-east-1a`, and its attached EBS volume is now available. Your teammate
tries to attach it to an EC2 instance in `us-east-1b` but he can't. What is a possible cause for this?
- [ ] He's missing IAM permissions
- [ ] EBS volumes are locked to an AWS Region
- [ ] EBS volumes are locked to an Availability Zone

<details><summary>Answer</summary>
<p>
  EBS volumes are locked to an Availability Zone
</p>
</details>

2). You have launched an EC2 instance with two EBS volumes, the Root volume type and the other EBS volume type to store
the data. A month later you are planning to terminate the EC2 instance. What's the default behavior that will happen to each EBS volume?
- [ ] Both the root volume type and the EBS volume type will be deleted
- [ ] The Root volume type will be deleted and the EBS volume type will not be deleted
- [ ] The root volume type will not be deleted and the EBS volume type will be deleted
- [ ] Both the root volume type and EBS volume type will not be deleted

<details><summary>Answer</summary>
<p>
  The Root volume type will be deleted and the EBS volume type will not be deleted
</p>
<p>
  By default, the Root volume type will be deleted as its Delete On Termination attribute is checked by default. Any other
  EBS volume types will not be deleted as its Delete On Termination attribute is disabled by default.
</p>
</details>

3). You can use an AMI in N.Virginia Region `us-east-1` to launch an EC2 instance in any AWS Region.
- [ ] True
- [ ] False

<details><summary>Answer</summary>
<p>
  False
</p>
<p>
  AMIs are built for a specific AWS Region, they're unique for each AWS Region. You can't launch an EC2 instance using an
  AMI in another AWS Region, but you can copy the AMI to the target AWS Region and then use it to create your EC2 instances.
</p>
</details>

4). Which of the following EBS volume types can be used as boot volumes when you create EC2 instances?
- [ ] gp2, gp3, io1, io2
- [ ] gp2, gp3, st1, sc1
- [ ] io1, io2, st1, sc1

<details><summary>Answer</summary>
<p>
  gp2, gp3, io1, io2
</p>
</details>

5). What is EBS Multi-Attach?
- [ ] Attach the same EBS volume to multiple EC2 instances in multiple AZs
- [ ] Attach multiple EBS volumes in the same AZ to the same EC2 instance
- [ ] Attach the same EBS volume to multiple EC2 instances in the same AZ
- [ ] Attach multiple EBS volumes in multiple AZs to the same EC2 instance

<details><summary>Answer</summary>
<p>
  Attach the same EBS volume to multiple EC2 instances in the same AZ
</p>
</details>

6). You have provisioned an 8 TB gp2 EBS volume, and you are running out of IOPS. What is NOT a way to increase performance?
- [ ] Mount EBS volumes in RAID 0
- [ ] Change to an io1 volume type 
- [ ] Increase the EBS volume size

<details><summary>Answer</summary>
<p>
  Increase the EBS volume size
</p>
<p>
  EBS IOPS peaks at 16,000 IOPS or equivalent 5334 GB
</p>
</details>

7). You have a fleet of EC2 instances distributes across AZs that process a large data set. What do you recommend to make
the same data to be accessible as an NFS drive to all of your EC2 instances?
- [ ] Use an Instance Store
- [ ] Use EBS
- [ ] Use EFS

<details><summary>Answer</summary>
<p>
  Use EFS
</p>
</details>

8). You would like to have a high-performance local cache for your application hosted on an EC2 instance. You don't mind
losing the cache upon the termination of your EC2 instance. Which storage mechanism do you recommend as a Solutions Architect?
- [ ] Instance Store
- [ ] EBS
- [ ] EFS

<details><summary>Answer</summary>
<p>
  Instance Store
</p>
<p>
  EC2 Instance Store provides the best disk I/O performance
</p>
</details>

9). You are running a high-performance database that requires an IOPS of 310,000 for its underlying storage. What do you recommend?
- [ ] Use an EC2 Instance Store
- [ ] Use an EBS gp2 drive
- [ ] Use an EBS io1 drive
- [ ] Use an EBS io2 Block Express drive

<details><summary>Answer</summary>
<p>
  Use an EC2 Instance Store
</p>
<p>
  You can run a database on an EC2 instance that uses an Instance Store, but you'll have a problem that the data will be
  lost if the EC2 instance is stopped (it can be restarted without problems). One solution is that you can set up a replication
  mechanism on another EC2 instance with an Instance Store to have a standby copy. Another solution is to set up backup
  mechanisms for your data. It's all up to you how you want to set up your architecture to validate your requirements.
  In this use case, it's around IOPS, so we have to choose an EC2 Instance Store.
</p>
</details>
