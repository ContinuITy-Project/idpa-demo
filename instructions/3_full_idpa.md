*[Back to contents](../README.md)*

## 3. Extending to Full IDPA

We now created an IDPA for a small excerpt of the Heat Clinic's API. For generating load tests, we base on the complete API. For this, we do the following:

1. Change the tag to not overwrite the changes before:
```
tag set heat-clinic
```

2. Create the full application model:
```
app create openapi/swagger-api-v1.json
```

3. Creating a full annotation for the Heat Clinic is out of the scope if this demo. Therefore, copy the already provided annotation at ```solutions/v1/annotation-heat-clinic.yml``` to ```cli-wd```.
4. You can double-check that the annotation is actually correct with ```ann check```.
5. Being convinced that the IDPA consisting of the application model and the annotation is complete and correct, we need to upload it to the ContinuITy tool, which will then use it to generate load tests. This needs to be done with the following two commands, executed one after the other:
```
app upload
ann upload
```

***[Continue with the next step...](4_load_test.md)***