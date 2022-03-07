# Configuration

## config\config.js
```js
module.exports = {
    // add the resource name that you need
    "Patient" : { 
        "interaction": {
            "read": true,
            "vread": true,
            "update": true,
            "delete": true,
            "history": true,
            "create": true,
            "search": true
        }
    }
}
```
!!! note
    此檔案在設定您所想支援的FHIR Resources(資源)。

    如果您想支援所有的FHIR Resources(資源)，您可以執行以下指令：
    ```sh
    node config/generate-allResources.js
    ```
    執行指令將會產生已設定所有FHIR Resource(資源)的config.js檔案

## dotenv
`.env` 於專案根目錄
```env
MONGODB_NAME="dbName"
MONGODB_HOSTS=["mongodb"]
MONGODB_PORTS=[27017]
MONGODB_USER="myAdmin"
MONGODB_PASSWORD="MymongoAdmin1"
MONGODB_IS_SHARDING_MODE=false
MONGODB_SLAVEMODE=false

SERVER_PORT=8080 

FHIRSERVER_HOST="localhost"
FHIRSERVER_PORT=8080 #use by creating bundle url
FHIRSERVER_APIPATH="fhir"

#If u want to use token auth, add below.
ENABLE_TOKEN_AUTH=true
ADMIN_LOGIN_PATH="adminLogin"  
ADMIN_USERNAME="adminUsername"
ADMIN_PASSWORD="adminPassword"

ENABLE_CHECK_ALL_RESOURCE_ID=false #true that want to check resource id cross all resource
ENABLE_CHECK_REFERENCE #true that want to check reference is exist in resource content

ENABLE_CSHARP_VALIDATOR=false 
VALIDATION_FILES_ROOT_PATH="FHIRValidatorAPI/FHIRValidatorAPI/assets/validationResources" # Please config the path corresponded to CSharp assets/validationResources directory
VALIDATION_API_URL="https://localhost:44381/api/validate"
```

## 產生程式碼
如果您已完成以上的設定，您必須執行以下指令產生 Mongoose Model、API 程式碼讓 Burni 正常運作。
```sh
npm run build
```
!!! warning
    `TypeError: genParamFunc[type] is not a function` 代表此類型的搜尋參數目前不支援。