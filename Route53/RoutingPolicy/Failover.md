We can have primary & secondary IP's to the same record.

This policy utilizes the health check feature of Route53 to return back IP.

In this policy, if primary is not passing health check, control is transfered to secondary and it returns back the secondary IP.

# Must
- To associate a health check with primary IP

# Can
- A Secondary IP can or can not have a health check associated with it 