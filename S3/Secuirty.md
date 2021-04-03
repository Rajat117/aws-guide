1. IAM based
    1. We have set IAM permissions on S3 or S3 bucket and its operation based on user and their role
2. Resource based
    1. Bucket Policies - The constraints applied through bucket through S3 console(Allows cross account access)
    2. Object Access Control List.
    3. Bucket Access Control List.

# Note:
An IAM principal can access the S3 object on(IAM based permission === true || resource policy ALLOW === true) && (There's explicit DENY === false)

# S3 Bucket Policies
Policies are stored as a json object with the default structure like this

```
{
    "Version": "2010-10-03",
    "Statement": [
        {
            "$id": "PublicRead",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::meribalti/*"
            ]
        }
    ]
}
```

# Terminologies in policy JSON
1. id - "A specific id to the permission",
2. Effect - Allow or Deny
3. Principal - The enitities which have permission for this policy.
4. Action - The operations allowed on this permission
5. Resource - The resource on which this permission applies to

# General use of bucket policy
1. Grant public access to bucket.
2. Forcing Encryption
3. Cross Account Access

# Additional Notes
1. We can expose S3 bucket in VPC without public internet(WWW) using VPC Endpoint
2. Logging & Audit 
    - S3 Access logs can be stored in another S3 bucket
    - API calls can be logged in AWS CloudTrail
3. User Security
    - MFA Delete: Functionality to delete an object only after MFA.
    - Pre-signed URL's: A url that can be made accessible only through authentication and for a limited amount of time.
