Create EKS cluster

```
aws eks create-cluster \
  --region us-west-2 \
  --name my-eks-cluster \
  --role-arn arn:aws:iam::123456789012:role/EKSClusterRole \
  --resources-vpc-config subnetIds=subnet-abc123,subnet-def456,securityGroupIds=sg-789xyz
  ```

  Create worker nodes

  ```
  aws eks create-nodegroup \
  --cluster-name my-eks-cluster \
  --nodegroup-name my-node-group \
  --subnets subnet-abc123,subnet-def456 \
  --instance-types t3.medium \
  --ami-type AL2_x86_64 \
  --scaling-config minSize=1,maxSize=5,desiredSize=3
  ```
