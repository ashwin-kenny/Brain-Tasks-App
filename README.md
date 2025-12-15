# React JS Nginx Image Deployed in EKS CLuster / CICD JENKINS / Terraform EC2, VPC, IAM

* This project contains the executable code of React JS deployed in EKS cluster.
* CICD using AWS Codebuild..

### Create EKS Cluster

eksctl create cluster
--name mindtrack-cluster
--region us-east-1
--version 1.34
--nodegroup-name c7i-flex-ng
--node-type c7i-flex.large
--nodes 1
--nodes-min 1
--nodes-max 1
--node-volume-size 20
--managed

### Create ECR Registry

* Search for ECR in AWS Management Console.
* Create Repository
* Provide the name of the repository 
* Click Create

 <img width="755" height="352" alt="image" src="https://github.com/user-attachments/assets/54627b22-c46d-4378-828c-131b0ae51e4b" />


### Create buildspec.yaml

https://github.com/ashwin-kenny/Brain-Tasks-App/blob/main/buildspec.yaml

### Create Deployment.yaml, service.yaml

https://github.com/ashwin-kenny/Brain-Tasks-App/blob/main/k8s/deployment.yaml

https://github.com/ashwin-kenny/Brain-Tasks-App/blob/main/k8s/service.yaml

### Create Codebuild Project

* Go to Codebuild-> Build Project -> Create Project
* Provide Project Name
* Select Source -> Github
* Create Credentials 
* Choose your Repository
* Select Use buildspec.yaml
* Enter “buildspec.yaml

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cacd7f0c-7d35-407f-a1b1-cd7713b02714" />

### Create Cloudwatch Logs (Already Incuded in Buildspec.yaml file)

* Create CLoudwatch Namespace
* kubectl create namespace amazon-cloudwatch
* Execute below command to enable the required loggings 

* aws eks update-cluster-config \
    --region 'us-east-1' \
    --name 'mindtrack-cluster' \
    --logging '{"clusterLogging":[{"types":["api","audit","authenticator","controllerManager","scheduler"],"enabled":true}]}'


* Create Fluent Bit Config Map Yaml file
* https://github.com/ashwin-kenny/Brain-Tasks-App/blob/main/k8s/fluent-bit-config-map.yaml
* Create Fluent BIt Service Account Yaml File
* https://github.com/ashwin-kenny/Brain-Tasks-App/blob/main/k8s/fluent-bit-sa.yaml
* Create Fluent Bit Daemonset Yaml File
* https://github.com/ashwin-kenny/Brain-Tasks-App/blob/main/k8s/fluent-bit-daemonset.yaml

### EKS Resources:

* Pods
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e0271d1a-d9ac-41ad-acfb-16ed82aa4c44" />


* Services

  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/684b20e1-e41c-41ac-b822-52843b21e178" />

* CloudWatch Logs
  
<img width="1902" height="929" alt="image" src="https://github.com/user-attachments/assets/6de2342d-0caf-4212-b8f5-91dd81e7b96b" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3f7a2424-ed0f-4b37-be43-54b9b725eb1c" />

<img width="1899" height="913" alt="image" src="https://github.com/user-attachments/assets/77210923-62fa-41ab-a4a1-9e439eaf04bd" />





### App Accessible on 8080 Port through LOAD BALANCER EXTERNAL IP

http://ac2361034298e48f9bf4539064a17677-1675241004.us-east-1.elb.amazonaws.com:8080

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0b85a4dd-3aec-4385-bb48-6cd70dd8cf07" />






