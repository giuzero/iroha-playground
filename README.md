# hato-iroha-playground
### just a playground to set up hato app
Create docker network
```
docker network create iroha-network;
```
Create postgres docker
```
docker run --name some-postgres \
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
Clone (need configuration files)
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
