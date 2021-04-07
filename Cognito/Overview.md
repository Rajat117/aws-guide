AWS service that lets you give identity to all the users outside your AWS. Let's say users in your web application

# Types
1. Cognito User Pools
## Intro
Creates a serverless database for you to manage your application user.
## Characteristic
- Simple Credential based Login (Email/Username & Password)
- Additional Attributes can also be stored (E.g. Name, Address etc)
- Password Reset
  - Can set constraints on password as well (E.g Min 6 letters)
- Phone & Email Verification
- MFA
- Federated Identities: Users from FB, Google, SAML, OpenId Connect
- Already hosted UI. (Can be customized easily)
- Can block users if their credentials are compromised
- On Login it returns back JWT.
## Events
We can perform any activity like triggering a lambda funcition on certain events (Pre authentication, Post Authentication, Pre Sign Up, Post Confirmation etc, etc)
## Integration
We can easily integrate it with
- API Gateway
- ALB 

2. Cognito Identity Pools (Federated Identity)
## Intro
Giving an identity to the bunch of users so that they can access AWS services.(Basically giving them temporary AWS credentials in exchange of credentials with constraints attached)
## Characteristic
- Identity Source can include
    - Federated Login
    - Users in Cognito User Pool
    - OpenID Connect & SAML Providers
    - Developer Authenticated Identities (Custom login)
    - Even a unauthenticated Guest Access
- Users have an IAM policy
- The same IAM policy can be customized based on the user_id or any entity you like which can be available as a variable to policy object.
- AWS services can then be accessed through API gateway or even directly(Say using SDK)

3. Cognito Sync (Deprecated)
## Intro
Used to store store preferences, config, state of app
## Characteristic
- Cross device synchronization
- Offline synchronization