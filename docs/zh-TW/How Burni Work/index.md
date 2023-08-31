# How Burni Work
本章節將告訴你 Burni 的工作原理

## Mongoose Model Generator
- Burni 的 Mongoose Model 主要由 FHIR 提供的 [FHIR JSON Schema](https://hl7.org/fhir/R4/fhir.schema.json.zip) 分析產生而成
1. 首先，因為 FHIR 底層都是以 Primitive Type (e.g. string, integer, boolean 等)組成，所以要先產生 Primitive Type 的程式碼
    - 不過，Burni 已經是程式碼產生完畢，若有興趣or核心出問題請自行查看原始碼
    - 主要程式碼可以在 `FHIR-mongoose-Models-Generator/PrimitiveGenerator.js` 中找到
2. 其餘資料型態 (i.e. General-Purpose, Metadata 以及 Special Purpose) 也已經被產生，若有興趣or核心出問題請自行查看原始碼
    - 主要程式碼可以在 `FHIR-mongoose-Models-Generator/ComplexGenerator.js` 中找到
3. Resource Type: 此為 Burni 產生 Mongoose 主要的 Data Type
    - Burni 會在你 `config/config.js` 設定的欄位進行產生相對應 Resource Type 的 Schema 程式碼
    - 主要程式碼可以在 `FHIR-mongoose-Models-Generator/resourceGenerator.js` 中找到
    - 產生的 Schema 都會放在 `models/mongodb/model` 當中

## API Generator
- Burni 會對你在 `config/config.js` 設定的 Resource Type，產生不同的 controller
- 主要程式碼可以在 `api_generator/API_Generator_V2.js` 找到
- 基本的 controller 如下
```js
const create = require('../../../FHIRApiService/create');
module.exports = async function(req, res) {
    return await create(req, res, "Account");
};
```

    - 你可以發現所有產生出來的都只會指向一個 function，這是因為要讓開發者能夠彈性的在不同的 Resource Type 更改其 controller (e.g. 增加前處理)

### Search Parameter Generator
- Burni 最複雜的就是 Search Parameter 的產生
1. 透過 [Search Parameter Registry](https://hl7.org/fhir/R4/searchparameter-registry.html) 抓取所有的 Search Parameter
2. 然後將每個 Search Parameter 做資料整理變成 `api_generator/FHIRParametersClean.json` 檔案
3. 每個 Search Parameter 都有 Type，透過 Type 去產生對應的程式碼
    - 主要程式碼可以在 `api_generator/searchParametersCodeGenerator.js` 以及 `api_generator/parameterHandler.js` 找到


## Search Parameter
- 每個 Resource Type 的 Search Parameter 處理器都可以在 `api/FHIR/${ResourceType}/${ResourceType}ParametersHandler.js` 找到
- 每種 Search Parameter 的核心組成 MongoDB Query 的程式碼可以在 `models/FHIR/searchParameterQueryHandler.js` 以及 `models/FHIR/queryBuild.js`


## APIs
- Burni 每一個 API 主要操作可以在 `api/FHIRApiService` 中找到，並且每個檔案名稱基本都與 FHIR 官方所提供的名稱一樣
