EKS cluster with 3-nodes

```
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  # Create a VPC
  MyVPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsSupport: true
      EnableDnsHostnames: true

  # Create Subnets
  PublicSubnetA:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref MyVPC
      CidrBlock: 10.0.1.0/24
      AvailabilityZone: us-west-2a
      MapPublicIpOnLaunch: true

  PublicSubnetB:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref MyVPC
      CidrBlock: 10.0.2.0/24
      AvailabilityZone: us-west-2b
      MapPublicIpOnLaunch: true

  # Create Security Group
  SecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: "Allow SSH and Kubernetes API access"
      VpcId: !Ref MyVPC
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 443
          ToPort: 443
          CidrIp: 0.0.0.0/0

  # Create an EKS Cluster
  EKSCluster:
    Type: AWS::EKS::Cluster
    Properties:
      Name: my-eks-cluster
      RoleArn: arn:aws:iam::123456789012:role/EKSClusterRole
      ResourcesVpcConfig:
        SubnetIds:
          - !Ref PublicSubnetA
          - !Ref PublicSubnetB
       
```
