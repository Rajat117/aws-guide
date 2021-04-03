You can look up for CORS onto the internet. Its same everywhere.

We have CORS in S3 in case one bucket object wants to fetch data from another bucket object.

Here is the sample configuration for adding CORS policy in S3 bucket

```
[
    {
        "AllowedHeaders": [
            "Authorization
        ],
        "AllowedMethod": [
            "GET"
        ],
        "AllowedOrigins": [
            "URL of bucket without slash at the end"
        ],
        "ExposeHeaders": [].
        "MaxAgeSeconds": 3000
    }
]
```