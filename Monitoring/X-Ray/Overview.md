X-Ray can be considered as an debugging utility. But the way it does that is so amazing that its not fair to say that it is only a debugging utility.
# Features
- You can analyse your application & its integration with other services in AWS visually.
- It gives us a visual as well as code level insight on what went wrong & on which service.
- We can track request behaviour
- Can check the latency for each api call.
- Understand dependancies in micro-service approach.
- Annotation can be added to provide extra info
- Security
    - KMS at rest
    - IAM (Obvious)
# Compatibility
- EC2 instance(Obvious thing) or any application server(even on-premise)
- Elastic BanStalk
- Lambda
- ECS
- API GateWay
- ELB
# How to enable it
- Using AWS X-Ray SDK in your code.
- Install the X-Ray daemon or enable AWS X-Ray integration
    - AWS Lambda(Lambda must have IAM execution role with proper policy) & some other services already run the X-Ray daemon.
# Sampling
Defining how much requests you want to record in X-Ray
- Reservoir - No of requests per second
- Rate - Additional requests
## Characteristic
- No need to restart on update.
## Smpling Rule
By Default 1 request per second(Reservoid) will be recorded & 5%(Rate) of any additional requests. 
## Must Know API
- `xray:PutTraceSegments`,
    - Upload segment document to X-Ray
    - necessary
- `xray: PutTelemetryRecords`,
    - Upload Segment metric
- `xray: GetSamplingRules`,
    - Retrieve all sampling ruls(that's why it don't need restart)
- `xray: GetSampling Targets`,
    - Related to sampling
- `xray: GetSamplingStatisticSummaries`
    - Related to sampling
- `GetServiceGraph` 
     - Main graph
- `BatchGetTraces`
    - Retrieves a list of
traces specified by ID. Each trace is a
collection of segment documents that
originates from a single request.
- `GetTraceSummaries`
    - Retrieves IDs
and annotations for traces available for
a specified time frame using an
optional filter. To get the full
traces,
pass the trace IDs to BatchGetTraces.
- `GetTraceGraph`
    - Retrieves a service
graph for one or more specific trace
IDs.
## X-Ray With BeanStalk
BeanStalk already include the deamon<br />
Options to enable it
- Using Console
- Using configuration file
    (
        In `.ebextensions/xray-daemon.config` use
    ```
    option_setting:
        aws::elasticbeanstalk:xray:
            XRayEnabled: true
    ```
    )
> Must: To give instance profile the correct IAM permissions
## X-Ray With ECS
- ECS Cluster
    - Container as a Daemon
        - Have to run daemon on each EC2 instance
    - Container as a SideCar
        - Have to run deamon on each app container in the EC2 instance.
- Fargate Cluster
    - Follows Container as a SideCar approach(Since we don't control instances there).
> Note: In the `dockerfile` for `x-ray daemon` specify `protocol` as `udp` under portMapping Key(Because daemon uses udp)
> Note: You must set env variable `AWS_XRAY_DAEMON_ADDRESS` to `Address of your x-ray daemon(e.g nameyouhavegiventox-ray-imageindocker:portonwhichitisrunning)` in your application dockerfile description, with a `links` object in application. Ref [Example task definition in this link](https://docs.aws.amazon.com/xray/latest/devguide/xray-daemon-ecs.html)

