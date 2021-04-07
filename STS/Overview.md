Allows to grant limited and temporary access to AWS resouces

# Must Know API
- AssumeRole
- AssumeRoleWithSAML
- AssumeRoleWithWebIdentity(Not used anymore)
- GetSessionToken
- GetFederationToken
- GetCalledIdentity
- DecodeAuthorizationMessage

# STS with MFA
- Use GetSesssionToken From STS
- Appropriate IAM policy
- Policy with condition
`"aws:MultiFactorAuthPresent": "true"`
- API returns
    - Session Token
    - Access ID
    - Secret Key
    - Expiration Date