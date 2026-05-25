# Day 13: Pull DVC-Tracked Data from Remote

## Task
 A new xFusionCorp Industries team member has cloned the fraud-detection repository onto a fresh machine. The DVC remote is already configured to point at the team's SeaweedFS bucket, but dvc pull is failing. Diagnose the cause, correct the configuration, and pull the dataset.


A cloned project exists at /root/code/fraud-detection/ with DVC initialised, the data/raw/transactions.csv.dvc pointer file present, but the dataset itself missing from disk and from the local DVC cache.

SeaweedFS is already running on the controlplane and the dataset has already been pushed to the dvc-storage bucket—open the SeaweedFS Filer button at the top of the lab and navigate to /buckets/dvc-storage/ to confirm that the object is there.

S3 endpoint: http://localhost:8333
Credentials: weedadmin / weedadmin123
Review .dvc/config and correct everything that prevents dvc pull from authenticating against SeaweedFS.

After the fix, the s3 remote must use:
The access key (access_key_id) weedadmin
The secret key (secret_access_key) weedadmin123.
Pull the dataset. After the pull, data/raw/transactions.csv must be present on disk and its content must match the hash recorded in the .dvc pointer.

## Solution

Inspect the current DVC remote configuration first:
```bash
cd /root/code/fraud-detection

cat .dvc/config
```

The file .dvc/config contains
```bash
[core]
    remote = s3

['remote "s3"']
    url = s3://dvc-storage
    endpointurl = http://localhost:8333
   
```


The file does not have all the configurations: the access key and the secret access key which are essential for connecting to the S3 bucket.
Configure the file correctly:
```bash
[core]
    remote = s3

['remote "s3"']
    url = s3://dvc-storage
    endpointurl = http://localhost:8333
    access_key_id = weedadmin
    secret_access_key = weedadmin123
```

Ensure all the credentials are correct(According to the specific instructions given ): 
- s3 access key - weedadmin
- s3 secret access key - weedadmin123
- s3 url - s3://dvc-storage
- s3 endpointurl - http://localhost:8333


After the credentials are set uo correctly, Pull the dataset from the s3 bucket
```bash
dvc pull
```

After the pull is successful verify the dataset exists and verify the contents:

```bash
ls data/raw/
```
This should return files in the raw folder and should contain a transaction.csv file

```bash 
cat data/raw/transactions.csv
```
The contents of the transaction.csv stored in the bucket should be listed:
```bash
transaction_id,amount,merchant,category,is_fraud
1001,25.50,StoreA,groceries,0
1002,1250.00,OnlineShopB,electronics,1
1003,45.00,RestaurantC,dining,0
1004,890.00,StoreD,clothing,0
1005,3200.00,OnlineShopE,electronics,1
1006,12.99,CafeF,dining,0
1007,560.00,StoreG,clothing,0
1008,78.50,GroceryH,groceries,0
1009,4100.00,OnlineShopI,electronics,1
1010,33.00,RestaurantJ,dining,0
1011,2750.00,OnlineShopK,electronics,1
1012,19.99,StoreL,groceries,0
```