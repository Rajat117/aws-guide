# Encyprtion in Transit
Data transfer b/w one source(Your pplication) to another(S3) in encrypted mode.

# Types
1. SSE-S3
- Uses keys handled & managed by AWS
- Algorithm - AES-256
- Must set Header `x-amz-server-encryption: AES256` on request.

2. SSE-KMS
- Uses AWS KMS to manage encryption keys
- KMS hanles the keys management for you but user have total control over how to use it.
- Must set Header `x-amz-server-encryption: aws:kms` on request.

3. SSE-C
- When user manages their keys themselves.
- User sends `encryption key` in headers for every S3 request.
- Encryption will still happen on server-side only the key you provided will be used

4. Client Side Encryption
- We send the encrypted data to S3
- We decrypt data retrived from S3.
- Full user control