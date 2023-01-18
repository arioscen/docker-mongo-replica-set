### Run
```
docker-compose up -d
```
### Check
```
docker-compose exec -it mongo1 mongosh --eval 'rs.status()'
```
### Reference:
* [deploying-a-mongodb-cluster-with-docker](<https://www.mongodb.com/compatibility/deploying-a-mongodb-cluster-with-docker>)