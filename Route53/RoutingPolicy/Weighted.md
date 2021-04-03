We can add multiple IPS to the same record(Though the AWS console will show you multiple record with the same name but at the end it is one).

Each record can be assigned a particular IP with the weight or we can say percentage of resolving to that IP.(We want our record to resolve to 12.12.12.12 - 70% times & 12.12.12.13 - 20% times).

The weight don't have to add up to 100.

The browser is not landed with the decision to chose IP becase it gets back only IP in the DNS lookup