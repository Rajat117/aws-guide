Bucket can be considedered as a main or root folder under which we store our files.

# Characteristic
- Operate at region level
- Naming Convenstion
    - Globally Unique
    - No uppercase
    - No underscore
    - 3-63 char long
    - Not an IP
    - Must start with lowercase or number
- Object(files) have a Key. E.g Key in `s3://bucket/object.txt` is `object.txt`
and Key in `s3://bucket/folder_1/object.txt` is `folder_1/object.txt`
- Max size for object = 5TB
- Max Upload Size = 5 GB
- Can have MetaData, Tags(Key/Value Pair)
- Can have VersionID(Versioning=True)