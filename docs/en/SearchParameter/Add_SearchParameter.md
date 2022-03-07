# Add search parameter
The code about search parameters can be found in `models\FHIR\queryBuild.js` and `models\FHIR\searchParameterQueryHandler.js` files. 

- `queryBuild.js`: get single MongoDB query object from data type.
- `searchParameterQueryHandler.js`: using `queryBuild.js` and get fully MongoDB query object from HTTP query param.

Some search parameters from generator will got missing or incorrect. You can fix by using methods in `models\FHIR\searchParameterQueryHandler.js`.

## Example: Bundle.composition
In some use cases, you may want to search `patient/{id}` in `entry.resource.subject.reference` of bundle resource.

- The example URL:
```sh
http://localhost:8080/fhir/Bundle?composition.patient=Patient/123
```
If you wanna support this parameter, you can add code in `api/FHIR/Bundle/BundleParametersHandler.js`.
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

