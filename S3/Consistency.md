S3 is made up of multiple servers. So when we write to S3 there can be a delay replicating the same data to other servers. Thats why S3 is evential consistent.

# Some analogy
U - You |
W - Write |
R - Read |
D - Delete |
O - Object

```
If (U-R-S3 && O-Exists) {
    "You will get 200 with the object data"
}
If (U-W-S3) {
    "You will get 200 with the successful write response"
}
If (U-R-S3-Now) {
    "You may or may not get the updated write"
}
```

```
If (U-W-S3 && O-DontExist) {
    "You will get 200 with the successful write response"
}
If (U-R-S3-Now) {
    "You will get 200 with the object data"(We dun have a outdated copy so this isonly possibility)
}
```

```
If (U-D-O-S3) {
    "You will get 200 with the successful write response"
}
If (U-R-S3-Now) {
    "You might get 200 with the object data for a short time"
}
```

# Note: No Strong Consistency yet in S3