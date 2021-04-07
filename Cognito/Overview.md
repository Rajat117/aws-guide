AWS service that lets you give identity to all the users outside your AWS. Let's say users in your web application

# Types
1. Cognito User Pools
## Intro
Creates a serverless database for you to manage your application user.
## Characteristic
- Simple Credential based Login (Email/Username & Password)
- Password Reset
- Phone & Email Verification
- MFA
- Federated Identities: Users from FB, Google, SAML, OpenId Connect
- Can block users if their credentials are compromised
- On Login it return back JWT.
## Integration
We can easily integrate it with
- API Gateway
- ALB 

2. Cognito Identity Pools (Federated Identity)
## Intro
Giving an identity to the bunch of users so that they can access AWS services.(Basically giving them temporary AWS credentials with constraints attached)
## Characteristic
- Identity Source can include
    - Federated Login
    - Users in Cognito User Pool
    - OpenID Connect & SAML Providers
    - Developer Authenticated Identities (Custom login)
    - Even a unauthenticated Guest Access
- Users have an IAM policy
- The same IAM policy can customized based on the user_id or any entity you like which can be available as a variable to policy object.

3. Cognito Sync
## Intro

## Characteristic