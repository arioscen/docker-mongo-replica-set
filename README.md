### Run
```
# 初始化
docker-compose -f init.yml up

# 新增工作資料夾
mkdir -p workspace/mongos

# 設定 keyfile
openssl rand -base64 756 > workspace/mongos/replkey
chmod 400 workspace/mongos/replkey
chown 999.root workspace/mongos/replkey

# 實際執行
docker-compose up -d
```
### Setting
進入 mongos 並使用 mongosh
```
$ docker-compose exec mongos bash
root@mongos:/# mongosh
```
在 mongosh 內
```
# 設定 root 使用者
admin = db.getSiblingDB("admin")
admin.createUser(
  {
    user: "admin",
    pwd: passwordPrompt(),
    roles: [ { role: "root", db: "admin" } ]
  }
)
# 驗證使用者
db.getSiblingDB("admin").auth("admin", passwordPrompt())

# 設定分片
sh.addShard("oneReplicaSet/first-shard-one:27018,second-shard-one:27018,third-shard-one:27018")

# 確認分片狀態
sh.status()
```
### Reference:
* [Deploying a MongoDB Cluster with Docker](<https://www.mongodb.com/compatibility/deploying-a-mongodb-cluster-with-docker>)
* [Update Replica Set to Keyfile Authentication](<https://www.mongodb.com/docs/manual/tutorial/enforce-keyfile-access-control-in-existing-replica-set>)