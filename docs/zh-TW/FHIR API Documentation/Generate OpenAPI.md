# 產生 OpenAPI
Burni 使用 [apidoc](https://apidocjs.com/) 以及在`config/config.js`檔案設定的Resources 產生 OpenAPI 文件。並使用[ReDoc](https://github.com/Redocly/redoc)作為API文件的網站.

!!! info
    API文件完整範例網站 [here](https://chinlinlee.github.io/Burni/apidoc/redoc/)

## 如何產生
- 使用下面的指令於`docs/apidoc/apidoc-sources`產生含有[apidoc]註解的檔案
```sh
node api_generator/doc-generator.js
```
範例：
```js
/**
     * 
     * @api {get} /fhir/Account/:id read Account
     * @apiParam {string} id Resource ID in server
     * @apiName readAccount
     * @apiGroup Account
     * @apiVersion  v2.1.0
     * @apiDescription read Account resource by id.
     * 
     * @apiExample {Shell} cURL
     * #example from: https://chinlinlee.github.io/Burni/assets/FHIR/fhir-resource-examples/account-example.json
     * curl --location --request GET 'http://burni.example.com/fhir/Account/0a2d866d-0362-4e05-9880-f62d054668cf'
     * @apiExample {JavaScript} javascript Axios
     //example from: https://chinlinlee.github.io/Burni/assets/FHIR/fhir-resource-examples/account-example.json
    const axios = require('axios');
    const config = {
        method: 'get',
        url: 'http://burni.example.com/fhir/Account/0a2d866d-0362-4e05-9880-f62d054668cf'
    };

    axios(config)
    .then(function (response) {
        console.log(JSON.stringify(response.data));
    })
    .catch(function (error) {
        console.log(error);
    });
    * @apiSuccess (Success 200 Content-Type: application/fhir+json) {object} FHIR-JSON-RESOURCE
    * @apiSuccessExample {json} (200) name: Success-Response Content-Type: application/fhir+json
    {
    "resourceType": "Account",
    "id": "0a2d866d-0362-4e05-9880-f62d054668cf",
    "identifier": [
        {
            "system": "urn:oid:0.1.2.3.4.5.6.7",
            "value": "654321"
        }
    ],
    "status": "active",
    "type": {
        "coding": [
            {
                "system": "http://terminology.hl7.org/CodeSystem/v3-ActCode",
                "code": "PBILLACCT",
                "display": "patient billing account"
            }
        ],
        "text": "patient"
    },
    "name": "HACC Funded Billing for Peter James Chalmers",
    "subject": [
        {
            "reference": "Patient/example",
            "display": "Peter James Chalmers"
        }
    ],
    "servicePeriod": {
        "start": "2016-01-01T08:00:00+08:00",
        "end": "2016-06-30T08:00:00+08:00"
    },
    "coverage": [
        {
            "coverage": {
                "reference": "Coverage/7546D"
            },
            "priority": 1
        }
    ],
    "owner": {
        "reference": "Organization/hl7"
    },
    "description": "Hospital charges",
    "meta": {
        "tag": [
            {
                "system": "http://terminology.hl7.org/CodeSystem/v3-ActReason",
                "code": "HTEST",
                "display": "test health data"
            }
        ],
        "versionId": "1",
        "lastUpdated": "2022-02-13T22:30:14.037+08:00"
    }
}
    * 
    * @apiSuccess (Success 200 Content-Type: application/fhir+xml) {object} FHIR-XML-RESOURCE
    * @apiSuccessExample {xml} (200) name: Success-Response-XML Content-Type: application/fhir+xml
    <?xml version="1.0" encoding="UTF-8"?><Account xmlns="http://hl7.org/fhir"><id value="69efa3c0-73b1-4403-ba4b-ffd7b718d053"/><meta><versionId value="1"/><lastUpdated value="2022-02-17T17:34:51.348+08:00"/><tag><system value="http://terminology.hl7.org/CodeSystem/v3-ActReason"/><code value="HTEST"/><display value="test health data"/></tag></meta><identifier><system value="urn:oid:0.1.2.3.4.5.6.7"/><value value="654321"/></identifier><status value="active"/><type><coding><system value="http://terminology.hl7.org/CodeSystem/v3-ActCode"/><code value="PBILLACCT"/><display value="patient billing account"/></coding><text value="patient"/></type><name value="HACC Funded Billing for Peter James Chalmers"/><subject><reference value="Patient/example"/><display value="Peter James Chalmers"/></subject><servicePeriod><start value="2016-01-01T08:00:00+08:00"/><end value="2016-06-30T08:00:00+08:00"/></servicePeriod><coverage><coverage><reference value="Coverage/7546D"/></coverage><priority value="1"/></coverage><owner><reference value="Organization/hl7"/></owner><description value="Hospital charges"/></Account>
    *
    * @apiError (Error Not Found 404 Content-Type: application/fhir+json) {object} FHIR-JSON-RESOURCE
    * @apiErrorExample {json} (404) name: Not-Found-Response Content-Type: application/fhir+json
    {
        "resourceType": "OperationOutcome",
        "issue": [
            {
                "severity": "error",
                "code": "exception",
                "diagnostics": "not found Account/0a2d866d-0362-4e05-9880-f62d054668cf"
            }
        ]
    }
    *
    * @apiError (Error Not Found 404 Content-Type: application/fhir+xml) {object} FHIR-XML-RESOURCE
    * @apiErrorExample {xml} (404) name: Not-Found-Response-XML Content-Type: application/fhir+xml
    <OperationOutcome xmlns='http://hl7.org/fhir'>
    <issue>
        <severity value='error'/>
        <code value='exception'/>
        <diagnostics value='not found Account/0a2d866d-0362-4e05-9880-f62d054668cf'/>
    </issue>
    </OperationOutcome>
    *
    */
```
- 使用以下指令在`docs/apidoc/redoc`產生 openAPI 文件
```sh
node docs/getAPIDocOpenapi.js
```
範例：
```json
{
    "openapi": "3.0.0",
    "servers": [
        {
            "url": "https://dev.burni.xn--7-c56d.com/"
        }
    ],
    "info": {
        "title": "Burni API documentation",
        "version": "v2.1.0",
        "description": "Documentation for the REST API"
    },
    "paths": {
        "/fhir/Account/{id}": {
            "get": {
                "operationId": "readAccount",
                "tags": [
                    "Account"
                ],
                "summary": "read Account resource by id.",
                "parameters": [
                    {
                        "name": "id",
                        "in": "path",
                        "required": true,
                        "schema": {
                            "type": "string"
                        },
                        "description": "Resource ID in server"
                    }
                ],
                "responses": {
                    "200": {
                        "description": "successful operation",
                        "content": {
                            "application/fhir+json": {
                                "schema": {
                                    "type": "object",
                                    "items": {
                                        "$ref": "#/components/schemas/FHIR-XML-RESOURCE"
                                    }
                                },
                                "examples": {
                                    "Success-Response": {
                                        "value": {
                                            "resourceType": "Account",
                                            "id": "0a2d866d-0362-4e05-9880-f62d054668cf",
                                            "identifier": [
                                                {
                                                    "system": "urn:oid:0.1.2.3.4.5.6.7",
                                                    "value": "654321"
                                                }
                                            ],
                                            "status": "active",
                                            "type": {
                                                "coding": [
                                                    {
                                                        "system": "http://terminology.hl7.org/CodeSystem/v3-ActCode",
                                                        "code": "PBILLACCT",
                                                        "display": "patient billing account"
                                                    }
                                                ],
                                                "text": "patient"
                                            },
                                            "name": "HACC Funded Billing for Peter James Chalmers",
                                            "subject": [
                                                {
                                                    "reference": "Patient/example",
                                                    "display": "Peter James Chalmers"
                                                }
                                            ],
                                            "servicePeriod": {
                                                "start": "2016-01-01T08:00:00+08:00",
                                                "end": "2016-06-30T08:00:00+08:00"
                                            },
                                            "coverage": [
                                                {
                                                    "coverage": {
                                                        "reference": "Coverage/7546D"
                                                    },
                                                    "priority": 1
                                                }
                                            ],
                                            "owner": {
                                                "reference": "Organization/hl7"
                                            },
                                            "description": "Hospital charges",
                                            "meta": {
                                                "tag": [
                                                    {
                                                        "system": "http://terminology.hl7.org/CodeSystem/v3-ActReason",
                                                        "code": "HTEST",
                                                        "display": "test health data"
                                                    }
                                                ],
                                                "versionId": "1",
                                                "lastUpdated": "2022-02-13T22:30:14.037+08:00"
                                            }
                                        }
                                    }
                                }
                            },
                            "application/fhir+xml": {
                                "schema": {
                                    "type": "object",
                                    "items": {
                                        "$ref": "#/components/schemas/FHIR-XML-RESOURCE"
                                    },
                                    "xml": {
                                        "name": "Account"
                                    }
                                },
                                "examples": {
                                    "Success-Response-XML": {
                                        "value": "<?xml version=\"1.0\" encoding=\"UTF-8\"?><Account xmlns=\"http://hl7.org/fhir\"><id value=\"69efa3c0-73b1-4403-ba4b-ffd7b718d053\"/><meta><versionId value=\"1\"/><lastUpdated value=\"2022-02-17T17:34:51.348+08:00\"/><tag><system value=\"http://terminology.hl7.org/CodeSystem/v3-ActReason\"/><code value=\"HTEST\"/><display value=\"test health data\"/></tag></meta><identifier><system value=\"urn:oid:0.1.2.3.4.5.6.7\"/><value value=\"654321\"/></identifier><status value=\"active\"/><type><coding><system value=\"http://terminology.hl7.org/CodeSystem/v3-ActCode\"/><code value=\"PBILLACCT\"/><display value=\"patient billing account\"/></coding><text value=\"patient\"/></type><name value=\"HACC Funded Billing for Peter James Chalmers\"/><subject><reference value=\"Patient/example\"/><display value=\"Peter James Chalmers\"/></subject><servicePeriod><start value=\"2016-01-01T08:00:00+08:00\"/><end value=\"2016-06-30T08:00:00+08:00\"/></servicePeriod><coverage><coverage><reference value=\"Coverage/7546D\"/></coverage><priority value=\"1\"/></coverage><owner><reference value=\"Organization/hl7\"/></owner><description value=\"Hospital charges\"/></Account>"
                                    }
                                }
                            }
                        }
                    },
                    "404": {
                        "description": "error",
                        "content": {
                            "application/fhir+json": {
                                "schema": {
                                    "type": "object",
                                    "items": {
                                        "$ref": "#/components/schemas/FHIR-XML-RESOURCE"
                                    }
                                },
                                "examples": {
                                    "Not-Found-Response": {
                                        "value": {
                                            "resourceType": "OperationOutcome",
                                            "issue": [
                                                {
                                                    "severity": "error",
                                                    "code": "exception",
                                                    "diagnostics": "not found Account/0a2d866d-0362-4e05-9880-f62d054668cf"
                                                }
                                            ]
                                        }
                                    }
                                }
                            },
                            "application/fhir+xml": {
                                "schema": {
                                    "type": "object",
                                    "items": {
                                        "$ref": "#/components/schemas/FHIR-XML-RESOURCE"
                                    },
                                    "xml": {
                                        "name": "OperationOutcome"
                                    }
                                },
                                "examples": {
                                    "Not-Found-Response-XML": {
                                        "value": "<OperationOutcome xmlns='http://hl7.org/fhir'>\n<issue>\n    <severity value='error'/>\n    <code value='exception'/>\n    <diagnostics value='not found Account/0a2d866d-0362-4e05-9880-f62d054668cf'/>\n</issue>\n</OperationOutcome>"
                                    }
                                }
                            }
                        }
                    }
                },
                "x-codeSamples": [
                    {
                        "lang": "Shell",
                        "source": "#example from: https://chinlinlee.github.io/Burni/assets/FHIR/fhir-resource-examples/account-example.json\ncurl --location --request GET 'http://burni.example.com/fhir/Account/0a2d866d-0362-4e05-9880-f62d054668cf'",
                        "label": "cURL"
                    },
                    {
                        "lang": "JavaScript",
                        "source": " //example from: https://chinlinlee.github.io/Burni/assets/FHIR/fhir-resource-examples/account-example.json\nconst axios = require('axios');\nconst config = {\n    method: 'get',\n    url: 'http://burni.example.com/fhir/Account/0a2d866d-0362-4e05-9880-f62d054668cf'\n};\n\naxios(config)\n.then(function (response) {\n    console.log(JSON.stringify(response.data));\n})\n.catch(function (error) {\n    console.log(error);\n});",
                        "label": "javascript Axios"
                    }
                ]
            }
        }
    },
    "components": {
        "schemas": {
            "FHIR-JSON-RESOURCE": {
                "properties": {}
            },
            "FHIR-XML-RESOURCE": {
                "properties": {}
            },
            "readAccount": {
                "properties": {
                    "id": {
                        "type": "string",
                        "description": "Resource ID in server"
                    }
                },
                "required": [
                    "id"
                ]
            }
        }
    }
}
```