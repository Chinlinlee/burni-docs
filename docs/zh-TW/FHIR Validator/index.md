# FHIR Validator
Burni 的 FHIR Validator 透過 Node.js 與 Java 融合的專案 [node-java-fhir-validator](https://www.npmjs.com/package/node-java-fhir-validator) 實現

!!! warning "注意事項"
    [node-java-fhir-validator](https://www.npmjs.com/package/node-java-fhir-validator) **請使用 0.2.0 版本**，後續版本還未整合至 Burni

    - node-java-fhir-validator 0.2.0 版本使用 [joeferner / node-java](https://github.com/joeferner/node-java)
    - 後續版本則是使用 [node-java-bridge](https://github.com/MarkusJx/node-java-bridge) 重現 [fhir-validator-wrapper](https://github.com/inferno-framework/fhir-validator-wrapper) 的功能


- Burni 放置 FHIR Validator 的路徑: `utils/validator`
    - `index.js`: 初始化引入 `utils/validator/igs` 資料夾中的 StructureDefinition (profile json file) 和 xxx.package.tgz (ig tgz file) 到 validator 的程式碼
    - `processor.js`: 實作 `validateResource` 的程式碼

## 哪些 API 使用了 FHIR Validator?
- create: 當 POST 資料時，會先進行驗證，驗證通過才會進行 create，反之回傳 422 錯誤
- update: 當 PUT 資料時，會先進行驗證，驗證通過才會進行 update，反之回傳 422 錯誤
- $validate: 驗證功能，通過返回 200，反之回傳 422 錯誤