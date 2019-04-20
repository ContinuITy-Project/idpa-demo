*[Back to contents](../README.md)*

## 1. Generating an Application Model

The first step when wirking with an IDPA is the definition of an application model. The application model describes the API of the application to be tested (in this case, the Heat Clinic) and will be referenced by the parameterizations. We use a very simplified version of the API for illustration purposes, but we will extend it to the full API in a later step. We will use an already existing [OpenAPI](https://www.openapis.org/) (a.k.a. Swagger API) specification to generate the application model. For this, enter the ContinuITy CLI and perform the following steps:

1. Each IDPA is labeled with a *tag*. Different tags allow to maintain IDPAs for different applications or environments. We can set one globally and the CLI will take care of propagating it:
```
tag set heat-clinic-simple
```
2. For convenience, the CLI allows to go to certain contexts, which allow to use sub commands directly. In our case, simply execute ```idpa```. Instead, you can append ```idpa``` before each command in the following. The prompt of the CLI should now look like this:
```
continuity/idpa (heat-clinic-simple):>
```
3. We provide a Swagger API at ```openapi/swagger-api-v1-simple.json```. We can now transform it to an application model:
```
app create openapi/swagger-api-v1-simple.json
```
4. A file ```application-heat-clinic-simple.yml``` will open in your editor with the content shown below. This is our created application model, for which we now need to define parameterizations in an annotation.
```yaml
---
&heat-clinic-simple timestamp: 2019-04-17T13-39-36-599Z
endpoints:
- !<http>
  &homeUsingGET domain: heat-clinic.com
  port: 80
  path: /
  method: GET
  protocol: http
- !<http>
  &hotSaucesOverviewUsingGET domain: heat-clinic.com
  port: 80
  path: /hot-sauces
  method: GET
  protocol: http
- !<http>
  &doLoginUsingPOST domain: heat-clinic.com
  port: 80
  path: /login_post.htm
  method: POST
  headers:
  - 'Accept: application/x-www-form-urlencoded'
  - 'Content-Type: application/x-www-form-urlencoded'
  parameters:
  - &doLoginUsingPOST_csrfToken_REQ_PARAM name: csrfToken
    parameter-type: REQ_PARAM
  - &doLoginUsingPOST_password_REQ_PARAM name: password
    parameter-type: REQ_PARAM
  - &doLoginUsingPOST_username_REQ_PARAM name: username
    parameter-type: REQ_PARAM
  protocol: http

```

***[Continue with the next step...](2_annotation.md)***