# Baseline Characteristic
- Latency 100-200ms
- Can handle 3500 PUT/COPY/POST/DELETE requests/second
- Can handle 5500 GET/HEAD requests/second.

# KMS Limitation
Since we use `GenerateDataKey` KMS API when we upload a file and `Decrypt` KMS API when we download a file, we are bound to entertain the limits of KMS as well.
## KMS Characteristic
- Rate limit is dependant on Region
- You can not request a quota increase.

# Optimization
- Multi-Part Upload
    - Recommended for files > 100MB
    - Must for > 5GB
    - Help in uploading file in parts.
- S3 Transfer Acceleration (Limited to upload only)
    - Use of AWS edge to reduce public network traffic.
    - Compatible with multi-part upload.
> Reading file
- Request data in chunks paralelly
- Request only partial chunk of data if only that is needed.
