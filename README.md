## Mongodb Setup Using Replica Sets

### Setting up Keys
* openssl rand -base64 756 > ${PWD}/rs_keyfile
* chmod 0400 ${PWD}/rs_keyfile
* chown 999:999 ${PWD}/rs_keyfile

### Starting replica
* docker compose up -d
* docker exec -it mongo1 bash
* mongosh -u root -p pass
* Start replica set
```
rs.initiate({_id: "rs0", version: 1, members: [{ _id: 0, host: "mongo1:27017" }, { _id: 1, host: "mongo2:27017" }, { _id: 2, host: "mongo3:27017" } ] } )
```

### Notes
* Network bridge required so that docker containers can communicate with each other
* connectionString: mongodb://root:pass@localhost:51901,localhost:51902,localhost:51903/?replicaSet=rs0&authSource=admin
* wait for some time to elect primary
