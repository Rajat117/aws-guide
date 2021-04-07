# Intro

# Clusters

# Task Definition
### Intro
Metadata in JSON form to tell ECS how to run Docker container (Kind of Dockerfile)
### Contains information about
- image name
- port binding for container & host
- memory & CPU required
- env var
- networking info etc
### Task Role 
IAM role to perform some aws requests

# ECS Service
Helps define no of task to run & how to run them.
## ECS Service Characteristic
- Helps run no of tasks across our desired no of EC2 instances.
- Can be linked to CLB/ALB/NLB
- Possible to setup ASG
- LB can be setup at creation time.
- CLB can't be setup for dynamic ports
## Use of Load Balancer
If we don't forward traffic of our container to a static manually chosen port we can use load balancer to help us with that.

# ECR
Private docker image repository managed by AWS.
## ECR Characteristic
Access is managed by IAM.
Docker commands are independent from ECR
## Login Commands
CLI V1: `$(aws ecr get-login --no-include-email --region eu-west-1)` - We have to run the output of this command thats y $
CLI V2: `aws ecr get-login-password --region eu-west-1 | docker login --username AWS --password-stdin repositroyUrl.amazonaws.com` 

# Fargate
Fargate overcomes the limitations of ECS cluster i.e provisioning a ec2 instance manually when we need to scale.
It is a serverless technology and we don't have to provision anything on our own instead Fargate will do that for us.
# Fargaate Characteristic
- No need to provision EC2 instance
- Just need to create a task definition, our container will run automatically.
- INcrease the task no to scale that's all there is to it.

