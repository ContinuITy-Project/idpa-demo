*[Back to contents](../README.md)*

## 2. Annotating the Application Model

For parameterizing the load tests we will generate later, we need to add an annotation to the application model. The annotation overrides certain static properties and defines input data to be used in each request. Do the following:

1. Initialize an empty annotation:
```
ann init
```

2. A file ```annotation-heat-clinic-simple.yml``` will open, which we now can fill with parameterizations. As it can be seen in the application model, the endpoints have the domain name *heat-clinic.com* and port number *80*. We change it to the domain and port of our test environment using *overrides*. For defining it application-wide, we can change the top-level ```overrides: []``` to the following, meaning that generated load tests should request the domain and port *localhost:8090*:
```yaml
overrides:
- HttpEndpoint.domain: localhost
- HttpEndpoint.port: 8090
```

3. As a next step, we consider input data. We can see in the application model that there is one endpoint ```doLoginUsingPOST``` that has parameters. When executing a load test, input data have to be used for these parameters. We start with the *username* parameter and define user names that should be used when logging in. As an example, we imagine the database of our test version of the Heat Clinic has user accounts *user-1@test.com* to *user-200@test.com*. We can easily define to use these accounts with a CounterInput. Replace the ```inputs: []``` line with the following:
```yaml
inputs:
- !<counter>
  &Input_username format: user-#@test'.'com
  scope: GLOBAL
  start: 1
  increment: 1
  maximum: 200
```

4. Then, we need to map the input to the *username* parameter. This is done by the ParameterAnnotation belonging to it, as follows:
```yaml
  - parameter: doLoginUsingPOST_username_REQ_PARAM
    input: *Input_username
    overrides: []
```

5. The same procedure can be repeated for defining the input data for the *password* parameter, using the pattern ```password-#```
6. Finally, we need input data for the *csrfToken*. This can be extracted from the responses of other requests, e.g., the *homeUsingGET* request. For that, we define an ExtractedInput. Here, the *pattern* is a regular expression that will be applied to the responses of *homeUsingGET*.
```yaml
- !<extracted>
  &Input_extracted_csrfToken extractions:
  - from: homeUsingGET
    pattern: <input name="csrfToken" type="hidden" value="(.*)"/></form>
```

7. The annotation is now complete. To check whether the annotation is correct and fits to the application model, run the following command:
```
ann check
```

8. Confirming the correctness, you should get the following output:
```yaml
---
violations: {}
```

The annotation model that has finally been created should look like the following:
```yaml
---
overrides:
- HttpEndpoint.domain: localhost
- HttpEndpoint.port: 8090
inputs:
- !<counter>
  &Input_username format: user-#@test'.'com
  scope: GLOBAL
  start: 1
  increment: 1
  maximum: 200
- !<counter>
  &Input_password format: password-#
  scope: GLOBAL
  start: 1
  increment: 1
  maximum: 200
- !<extracted>
  &Input_extracted_csrfToken extractions:
  - from: homeUsingGET
    pattern: <input name="csrfToken" type="hidden" value="(.*)"/></form>
endpoint-annotations:
- endpoint: homeUsingGET
  overrides: []
  parameter-annotations: []
- endpoint: hotSaucesOverviewUsingGET
  overrides: []
  parameter-annotations: []
- endpoint: doLoginUsingPOST
  overrides: []
  parameter-annotations:
  - parameter: doLoginUsingPOST_csrfToken_REQ_PARAM
    input: *Input_extracted_csrfToken
    overrides: []
  - parameter: doLoginUsingPOST_password_REQ_PARAM
    input: *Input_password
    overrides: []
  - parameter: doLoginUsingPOST_username_REQ_PARAM
    input: *Input_username
    overrides: []
```

***[Continue with the next step...](3_full_idpa.md)***