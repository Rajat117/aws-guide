It means our data will get encrypted on flight. 

# Characeristic
- Basic need & must is SSL certification for this.
- Provide SSL options with trust certificate when connecting to DB.
- To encfore SSL
 - PostgresSQL - Set rds.force_ssl=1 in AWS console
 - MySQL - `GRANT USAGE ON *.* TO 'mysqluser'@'%' REQUIRE SSL`
 