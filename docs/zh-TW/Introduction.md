# 介紹
## Burni FHIR Server
Burni 使用 Node.JS 、Express 框架以及 MongoDB 實作 FHIR R4 Server，經由簡單的設定即可產生指定 FHIR Resource的 Mongoose Schema、API程式碼並可自行更改，滿足需求。目前Burni支援Windows以及Linux，讓開發人員可以快速架設 FHIR Server。

Burni 所使用的 FHIR 版本為 v4.0.1。

## Server 能力聲明
Burni 使用 AEGIS Touchstone Basic-R4-Server 測試. 

測試結果: 

- [FHIR4-0-1-Basic-Server version 18](https://touchstone.aegis.net/touchstone/conformance/detail?suite=FHIR4-0-1-Basic-Server&sVersion=18&testSystem=5f9518730a120e4edef042ae&supportedOnly=false&cb=%2fFHIR4-0-1-Basic&format=ALL&published=true) (2,216 tests has been passed, 100% Pass)
- [FHIR4-0-1-Basic-Server version 14](https://touchstone.aegis.net/touchstone/conformance/detail?suite=FHIR4-0-1-Basic-Server&sVersion=14&testSystem=5f9518730a120e4edef042ae&supportedOnly=false&cb=%2FFHIR4-0-1-Basic&published=true) (1,948 tests has been passed, 100% Pass)