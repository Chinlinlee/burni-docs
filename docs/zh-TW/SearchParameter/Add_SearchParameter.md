# 自行新增搜尋參數
與搜尋參數相關的程式碼位於`models\FHIR\queryBuild.js` 以及 `models\FHIR\searchParameterQueryHandler.js` 檔案。 

- `queryBuild.js`: 根據不同的 Data Type 組成單個MongoDB 查詢語法。
- `searchParameterQueryHandler.js`: 根據 HTTP 網址中的查詢條件使用 `queryBuild.js` 取得完整的 MongoDB 查詢語法。

由產生器產生之部分搜尋參數可能是錯誤的或遺失。您可以使用 `models\FHIR\searchParameterQueryHandler.js` 內的方法修正。

## 範例： Bundle.composition
在一些使用案例，您也許會想使用 bundle 的 `entry.resource.subject.reference` 搜尋 `patient/{id}`。

- The example URL:
```sh
http://localhost:8080/fhir/Bundle?composition.patient=Patient/123
```
如果您想支援此項搜尋參數，您可以在 `api/FHIR/Bundle/BundleParametersHandler.js` 檔案新增以下程式碼
```js
//#region composition.patient
// search parameter name: "composition.patient"
// field in resource: "entry.resource.subject.reference"
// type: reference
paramsSearchFields["composition.patient"]= ["entry.resource.subject.reference"];
paramsSearch["composition.patient"] = (query) => {
    try {
        queryHandler.getReferenceQuery(query, paramsSearchFields, "composition.patient");
    } catch (e) {
        console.error(e);
        throw e;
    }
};
//#endregion
```

