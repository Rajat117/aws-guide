A api gateway is a wall standing b/w your applications & traffic. You are going to your instances through the api gateway filter.

# Characteristic
- Versioning
- Multiple Env (dev, test, prod)
- Handle Authorization, Authentication
- Support for Swagger & Open API
- Caching, Throttling
- Generate specifications for SDK & API
- Support for AWS Lambda, WebSocket Protocol

# Integrations with
- Lambda Function
- HTTP (Expose API's in your backend)
- AWS Service

# Endpoint Types
- Edge-Optimised:
Deployed in one region but easily accessible on all edge location
    - For global clients
    - Reduces Latency(Since requests are routed through CloudFront Edge Location)
- Regional:
For handling users in the same region.
    - Can be manually combined with CloudFront to have more control over caching, response transforming, rate limiting etc.
- Private
It is deployed within the VPC where we dunn wanna expose it to the public internet(WWW)
    - Can only be accessed from the VPC using ENI

# Deployment
After we integrate our APIGateway with whatever the entity you want, we must deploy it(Even when we do code change, we will have to deploy it)

# Deployment Stages
Deployment stages can be considered as an environment for our application (dev, staging. prod)
## Stage Characteristic
- You can create any number of stages.
- Each stage has its own configuration parmeters
- Can be rolled back to previous deployment 
## Stage Variable
Kind of an env variable for your integrated service.
We can use this variable to route traffic to our different lambda functions or applications.
> Note: You will have to create resource based policy to allow access from your gateway to a resource when allowing dynamic access

# Canary Deployment
By Canary Deployment we can allow only some % of the traffic to be redirected to our canary stage while rest can go to normal stage.
## Canary Characteristic
- Monitoring & logs are separate
- Can override stage varibale for canary
- Canary can be promoted later to the main stage

# Mapping
> Prerequisite: If you will do a hands on of APIGateway, you will see that there is always an option to proxy request directly to integration type.

Mapping is changing request & response(headers, payload etc)as per the need of your application or any other scenario.

> Note: Mapping is done by `VTL: Velocity Template Language`
## For Proxy Based Integration
We can't use mapping of request & response(be it payload, query string param, header) since it directly goes to integrated entity
## For Non Proxy Based Integration
We can use mapping of request & response.
E.g Converting SOAP payload from client to JSON format & pass it to integrated entity & return the JSON response from integrated entity back to the client.

# Caching in APIGateway
- Default TTL = 300s. Max = 3600s. Min = 0s
- Defined per stage
- Can be overriden for a particular method as well
- Encryption possibility
- Capacity = 0.5GB - 237GB
- Expensive operation
## Invalidate Cache
- We can flush it from console
- Clients can invalidate if they set header
`Cache-Control: max-age=0` (Only if authorized or no authorization is required to invalidate it)


