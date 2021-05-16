# Authorization Model Evaluation Of Policies

let's understand it with if else condition

```
var explicitDeny = `True/False`;

let DENY=false;

const isAllowedFromEvaluation = EvaluateAllApplicablePolicies();

if (explicitDeny === 'True') {
    return false;
} else {
    if (isAllowedFromEvaluation === 'True') {
        return true;
    } else {
        return false;
    }
}
```

# IAM Policies & S3 Bucket Policies
Its as simple as this

const isAllowedFromEvaluation = IAMPolicyEvaluation() U(Union) S3BucketPolicy();

# Dynamic Policies with IAM
Make policies dynamic by using env or dynamically available variable.
E.g One Policy that give user access to bucket with their username only.
```
{
    $id: "AllowActionInS3",
    Action: ["s3.*"],
    Effect: "Allow",
    Resource: ["arn::s3:::bucket/${aws:username}/*"]
}
```

# Inline Vs Managed Policy
| Managed                                | Customer Managed                | Inline                                        |
|:--------------------------------------:|:-------------------------------:|:---------------------------------------------:|
| Manatained By AWS                      | Fully control & managed by user | Strict 1-to-1 relnship b/w policy & principal | 
| Suitable for admin level user          | Re-usable                       | Policy is deleted if you delete principal     | 
| Updated in case of new service/new API | Version controlled + Rollback   |                                               |
|                                        | Best practice                   |                                               | 

# Granting a User Permission to Pass a Role to an AWS Service.
- Must attach IAM permission `iam:PassRole` to user
- You should also attach `iam:GetRole` to view the role
E.g this policy means User can only Pass S3 role to AWS service
```
{
    Version: "2028-10-19",
    Statement: {
        {
            Effect: "Allow",
            Action: "iam:PassRole",
            Resource: "arm/whatever/S3Access"
        }
    }
}
```

> Note: Roles can be passed on the basis of what their servies's trust allows.(There is a trust relationship b/w aws service. You might be able to see it in the console). 