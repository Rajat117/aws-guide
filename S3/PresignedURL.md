Command to do that
`aws s3 presign s3://meribalti/myobject --region my-region`

To add a custom expiration time (Default is 3600s).
`aws s3 presign s3://meribalti/mmyobject --expires-in 300 --region my-region`

Set the proper signature version in order to no to get issues when gnerating URL's for encrypted files
`aws configure set default.s3.signature_version s3v4`