# Steps to Enable Replica Set in MongoDB

## 1. Modify MongoDB Configuration File
Edit the MongoDB configuration file (usually located at /etc/mongod.conf on Linux).

```yaml
replication:
  replSetName: "rs0"
  ```

## 2. Restart MongoDB
Restart the MongoDB service to apply the changes.

```sh
sudo systemctl restart mongod
```

## 3. Initialize the Replica Set
Start the MongoDB shell and initiate the replica set.

```sh
mongo
```

In the MongoDB shell, run the following commands:

```js
rs.initiate()
```

You should see a response indicating the replica set has been initiated.
Example of MongoDB Configuration (mongod.conf)

Here’s a full example of a typical mongod.conf with the replica set configuration:

```yaml
# mongod.conf

# Where and how to store data.
storage:
  dbPath: /var/lib/mongo
  journal:
    enabled: true

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1

# how the process runs
processManagement:
  timeZoneInfo: /usr/share/zoneinfo

# Enable the replica set
replication:
  replSetName: "rs0"
```

## 4. Confirming the replica set 
After initiating the replica set, you can check its status with:

```js
rs.status()
```

# Using MongoDB Transactions in Spring Data MongoDB
With the replica set enabled and initialized, your Spring Data MongoDB application should now be able to perform transactions. Ensure your application connects to the MongoDB instance using the correct URI for a replica set.

**Example URI in application.properties**

```sh
spring.data.mongodb.uri=mongodb://localhost:27017/mydatabase?replicaSet=rs0
```

## Summary
- Enable and configure the replica set in mongod.conf.
- Restart MongoDB.
- Initialize the replica set using rs.initiate().
- Ensure your Spring Boot application connects to MongoDB using the correct URI.

With these steps, your MongoDB instance should be properly configured to support transactions.