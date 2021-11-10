# iroha-playground
## just a playground
Create docker network
```
docker network create iroha-network;
```
Create postgres docker
```
docker run --name postgres4iroha \
-e POSTGRES_USER=postgres \
-e POSTGRES_PASSWORD=mysecretpassword \
-p 5432:5432 \
--network=iroha-network \
-d postgres:9.5 \
-c 'max_prepared_transactions=100'
```
Create blockstore
```
docker volume create blockstore
```
Clone
```
git clone -b main https://github.com/hyperledger/iroha --depth=1
```
Start iroha container
```
docker run --name iroha \
-d \
-p 50051:50051 \
-v $(pwd)/iroha/example:/opt/iroha_data \
-v blockstore:/tmp/block_store \
--network=iroha-network \
-e KEY='node0' \
hyperledger/iroha:latest
```
