It means you can set the encryption strategy at the time of launching the databse.

# Characeristic
- Possibility to encrypt master and read replica with AWS KMS(Key Management Service)(Mostly Used for encryption purpose). It uses AES 256 encryption.
- If (Master != encrypted) { Replica can-not be encrypted }
- ORACLE and SQL Server hage TDE (Transparent Data Encryption)encryption available 