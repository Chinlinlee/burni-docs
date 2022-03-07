# 部屬
## 使用 Node.JS
```sh
node server.js
```
您會看到 console 打印以下訊息：
```
mongodb://localhost:27017/dbName
moduleName ::  Patient
path :  path\burni\models\mongodb/model
moduleName ::  Patient_history
path :  path\burni\models\mongodb/model
moduleName ::  FHIRStoredID
path :  path\burni\models\mongodb/staticModel
moduleName ::  issuedToken
path :  path\burni\models\mongodb/staticModel
http server is listening on port:8089
we're connected!
```
## 使用 docker-compose
以下是來自根目錄 `docker-compose.yaml` 的範例
```yaml
version: '3.4'
services:
  fhir-burni-mongodb:
    image: mongo:4.2
    container_name : fhir-burni-mongodb
    restart: always
    ports:
      - 27017:27017
    volumes:
      - ./mongodb/db:/data/db
    environment:
      # provide your credentials here
      - MONGO_INITDB_DATABASE=admin
      - MONGO_INITDB_ROOT_USERNAME=root
      - MONGO_INITDB_ROOT_PASSWORD=root
      - MONGO_PORT=27017
  
  fhir-burni:
    build: ./
    container_name: fhir-burni
    command: >
      /bin/sh -c '
      while ! nc -z fhir-burni-mongodb 27017;
      do
        echo "waiting for database ...";
        sleep 3;
      done;
      echo "db is ready!";
      pm2-runtime start ecosystem.config.js;
      '
    volumes :
      - ./:/nodejs/fhir-burni
      - /nodejs/fhir-burni/node_modules
    ports:
      - 8080:8080
    depends_on:
      - fhir-burni-mongodb
    tty : true
    restart: on-failure:3
    stdin_open : true
```
### docker-compose部屬
```sh
docker-compose up -d
```