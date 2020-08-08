# jmeter-stuffs
1. Validate json schema using external libraries and JSR223
  - Select appropriate versions of the following libs, puth them in /lib folder of your jmeter instalation
      - https://github.com/stleary/JSON-java
      - https://github.com/everit-org/json-schema
      - https://github.com/damnhandy/Handy-URI-Templates
  - Add the following code to JSR223 script section:
    ```
    def schemaPath = '/path/to/your/schema.json'
    def rawSchema = new org.json.JSONObject(new org.json.JSONTokener(org.apache.commons.io.FileUtils.readFileToString(new File(schemaPath), 'UTF-8')))
    def schema = org.everit.json.schema.loader.SchemaLoader.load(rawSchema)
    schema.validate(new org.json.JSONObject(prev.getResponseDataAsString()))
    ```
    Credits to Dmitri T. at https://stackoverflow.com/questions/54575805/how-can-i-write-json-schema-validation-for-jmeter-run-in-teamcity
