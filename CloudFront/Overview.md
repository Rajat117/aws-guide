# Intro
A CDN - Content Delivery Network.The basic idea is the use of edge locations(There are around 216 aws edge location) to cache the content and deliver content from there as soon user uses second fetch or second request.

# Characteristic
- TTL. `Min = 0s` | `Max = 1 year`
- Can expose external HTTPS
- Can talk to internal HTTP/HTTPS backend.
- Viewer Protocol Policy.
  - Allow any HTTP or HTTPS
  - Redirect HTTP to HTTPS
  - Use only HTTPS
- Origin Protocol Polic. (Origin is S3 or your HTTP backend from which u request resource)
  - HTTPS only
  - Match Viwer: HTTP -> HTTP || HTTPS -> HTTPS
- > Note: S3 Bucket dunn support HTTPS.
- Can restrict the allowed method (OPTIONS, GET, HEAD, POST, PUT, DELETE PATCH)
- Can also be used as in ingres(allow incoming traffic to save data on target origin)
- Cache
  - Based On
    - Headers
    - Session Cookies
    - Query String Params
  - Invalidate API
    - `CreateInvalidation`

> Note: It is better strategy to separate dyanmic & static distribution for max cache hits.
  
# OAI (Origin Access Identity)
It is basically assigning an idenity to the cloudFront so that it can be referenced as a Principal in the bucket policy & policy can allow access from it.
E.g `123456QWERTY` is the id here.
```{
  "Version": "2008-10-17",
  "Id": "PolicyForCloudFrontPrivateContent",
  "Statement": [
    {
      "Sid": "1",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity 123456QWERTY"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-content-through-cloudfront/*"
    }
  ]
}
```

# Origin
- S3
  - Uses OAI(Origin Access Identity) for authentication & authorization
- Anything that respects HTTP protocol
  - List
    - EC2 instace
    - ALB
    - APIGateWay (Not damn sure about it. But it should be valid as well).
    - S3 Static Website
    - Any HTTP API
  - They must allow incoming traffic from cloudfront IP's in their SG(Security Group).

# GEO Restriction
Based on user's IP, cloudFront can identify country & can 
- BlackList
- Whitelist

# CloudFront Signed Url
- Create a private url of the requested resource based on user's session key, header or public/private key basis.
- There are  2 ways to generate pre-signed url in cloudfront
  - Uploading public key [MustBe2048Bit] to the cloudfront & signing urls using private key securely stored in your backend.
  - Use CloduFront Key/Pair [OnlyRootUserCanGenerateIt] to create signed url using the sdk or api.

# To Remember Points
- Cost vary per region basis
- More Data Transfered - Less cost.
## Price Classes
- All
    - Includes all regions.
    - Best Practice
- 200
    - Most Regions, But Excludes the Most Expensive One
- 100
    - Only the Least Expensive Ones.
## Multiple Origin
We can route to different origin based on the content type of request. We can set a cache behaviour that does this separation of concern.
E.g Based on Path Pattern
- /api/* - ALB
- /images/* - S3.
## Origin Groups
Can set more than 1 origin as a target for a particular request.
In case of failover. any other origin could become the main origin.
## Field Encryption
Edge location can also encrypt sensitive data coming to it with the public key we have uploaded to it.
Only the backend with private key can then decrypt the data. Nothing in b/w. 