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
- LB can be setup only at creation time.
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
- Increase the task no.'s to scale that's all there is to it.

# ECS IAM 
## EC2 Instance Profile
- Used by the ECS agent to register it into ECS.
- Makes API calls to the ECS Service.
- Send logs to CLoudWatch.
- Pull images from ECR.
## ECS Task Role
- You must allow each task to have a specific role
- Use different roles for different ECS services

# ECS Task Placement
It is a strategy you can use to determine how & where to place your tasks in your ECS cluster normally as well as when the Cluster scales In & Out.
> Note: Not available for ECS Fargate (Fargate manages tasks on its own).
## AWS procedure for task placement
- Identifying instances that satisfy 
    - CPU, memory & port requirement.
    - Task placement constraint.
    - best the task placement strategies.
## Task Placement Strategy
- BinPack
    - Tries to load containers on the same instance unitll it gets fully packed & then allocate another instance & follow the same procedure
    ```
    PlacementStrategy: [
        {
            field: "memory", (Based on memory)
            type: "binpack"
        }
    ]
    ```
    - Cost Saving
- Random
    - Randomly placing containers(tasks) on the EC2 instance provisioned.
    - Not optimised but not bad either.
    ```
    PlacementStrategy: [
        {
            type: "random"
        }
    ]
    ```
- Spread
    - Evenly spread task across instances based on certain attribute. e.g. based on availability zones.
    ```
    PlacementStrategy: [
        {
            field: "attribute:ecs.availability-zone",
            type: "spread"
        }
    ]
    ```
> Note: These strategies can be mixed together

## ECS Task Placement Constaints
- distinctInstance
     ```
    PlacementConstraints: [
        {
            type: "distinctInstance"
        }
    ]
    ```
- memberOf
    ```
    PlacementConstraints: [
        {
            field: "attribute:ecs.availability-zone =~ t2.*",
            type: "memberOf"
        }
    ]
    ```

# ECS Auto Scaling
> Note: ECS Service Scaling(task level) != EC2 Auto Scaling(instance level)

# ECS Cluster Capacity Provider
Since ECS Service Scaling is as scaling at the task level, it dunn provision new instance when all the instances in the cluster are at full capacity. So to solve this we can use Cluster Capacity Provider which when attached with task will create a new instance(EC2 or Fargate(whichever you choose)) for you if current capacity is not sufficient to handle task load.
