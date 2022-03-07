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
    This file is config what resources you want to support.
    
    If you want to support all resources, you can run command below:
    ```sh
    node config/generate-allResources.js
    ```
    This will generate config.js for all resources.

## dotenv
`.env` in root path.
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

## Generate code
After configuration above, you need to run script below to generate js code of API and mongoose model.
```sh
npm run build
```
!!! warning
    `TypeError: genParamFunc[type] is not a function` is meaning that method of search parameter not support now.