ELB - Elastic Load Balancer
# Intro
ELB's are AWS managed load balancer.It takes a great effort to setup a normal load balancer yourself but since ELB by AWS is already a managed service, we are left to do very minimal configurations.
# Types
## Classic LB
- Deals In
  - HTTP, HTTPS (Layer 7), TCP (Layer 4)
## Application LB
### Deals In
  - HTTP, HTTPS, WebSocket (Layer 7)
### Characteristic
  - Support redirects from HTTP to HTTPS
  - Latency (~400ms)
  - Routing based on
    - Path in URL
    - Hostname in URL
    - Headers
    - & Even query strings,
  - Port mapping feature to redirect to dynamic port.
  - ALB Target Groups (Group of enitities to redirect traffic to)
    - EC2 instances
    - ECS Tasks
    - Lambda Fn
    - IP Addresses (Only Private IP's)
## Network LB
- Deals In
  - TCP, TLS (Secure TCP) & UDP (Layer 4)
### Characteristic
  - Handles millions on req/seconds
  - Low latency (~100ms)
  - Has one static IP/AZ
  - Suuport Elastic IP
## GateWay LB
- Don't have anough info at the moment. Will add it surely.
# Characteristic
- Internal(private network facing) & External(public network facing) LB
# Stickiness
- Always Redirecting traffic to a particular instance behind the LB
## Use Case
- Session based app
## Limitation
- ALB & CLB
# Cross Zone Load Balancing
- Distributing load across all EC2 instances in each zone evenly.
## ELB's Intra AZ
- CLB
  - Enabled (By Default)
  - Free
- ALB
  - Always On (Can't be disabled)
  - Free
- NLB
  - Disabled (By Default)
  - Not Free
# SNI
Allows you to load multiple SSL certificate on 1 web server
> Note: Only works for ALB & NLB