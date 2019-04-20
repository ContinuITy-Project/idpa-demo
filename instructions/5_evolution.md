*[Back to contents](../README.md)*

## 5. Evolving the IDPA over API changes

Commit [010f8a2 at August 3, 2017](https://github.com/BroadleafCommerce/DemoSite/tree/010f8a27e98a32eee14106bf904414d3d9296892) of the Heat Clinic's commit history introduced a set of API changes. Hence, if we would like to generate load tests for the new API version, we need to adjust our IDPA. The first step in doing so is to update the application model. This can be done based on a Swagger API we provide in ```openapi/swagger-api-v2.json``` with the following command:
```
app update openapi/swagger-api-v2.json
```

The command will open a file ```application-heat-clinic.yml``` containing the new application model. Also, it will open ```application-heat-clinic-old.yml``` containing the old version for comparison. The output at the command line will be a list of API changes between the two versions:
```yaml
Updated with openapi/swagger-api-v2.json:
---
beforeChange: 2019-04-17T13-36-52-874Z
afterChange: 2019-04-17T13-56-45-873Z
application-changes:
- message: 'Parameter added: A new parameter has been added.'
  changed-element:
    type: HttpParameter
    id: doLoginUsingPOST_r_me_REQ_PARAM
- message: 'Endpoint added: A new endpoint has been added.'
  changed-element:
    type: HttpEndpoint
    id: pricingSummaryUsingGET
- message: 'Parameter removed: The parameter has been removed.'
  changed-element:
    type: HttpParameter
    id: saveSingleShipUsingPOST__useBillingAddress_REQ_PARAM
- message: 'Endpoint added: A new endpoint has been added.'
  changed-element:
    type: HttpEndpoint
    id: miniCartUsingGET
- message: 'Parameter added: A new parameter has been added.'
  changed-element:
    type: HttpParameter
    id: saveSingleShipUsingPOST_a_postalCode_REQ_PARAM
- message: 'Parameter added: A new parameter has been added.'
  changed-element:
    type: HttpParameter
    id: saveSingleShipUsingPOST_a_addressLine1_REQ_PARAM
- message: 'Endpoint added: A new endpoint has been added.'
  changed-element:
    type: HttpEndpoint
    id: updateQuantityFromWishlistUsingPOST
- message: 'Endpoint removed: The endpoint has been removed.'
  changed-element:
    type: HttpEndpoint
    id: saveBillingAddressUsingPOST
- message: 'Parameter added: A new parameter has been added.'
  changed-element:
    type: HttpParameter
    id: saveSingleShipUsingPOST_a_fullName_REQ_PARAM
- message: 'Parameter added: A new parameter has been added.'
  changed-element:
    type: HttpParameter
    id: saveSingleShipUsingPOST_a_city_REQ_PARAM
- message: 'Parameter removed: The parameter has been removed.'
  changed-element:
    type: HttpParameter
    id: saveSingleShipUsingPOST_useBillingAddress_REQ_PARAM
- message: 'Parameter added: A new parameter has been added.'
  changed-element:
    type: HttpParameter
    id: saveSingleShipUsingPOST_a_stateProvinceRegion_REQ_PARAM
- message: 'Endpoint added: A new endpoint has been added.'
  changed-element:
    type: HttpEndpoint
    id: viewCustomerPaymentsUsingGET
```

If we now check the validity of the annotation model with ```ann check```, we will see several violations, such as
```yaml
null [EndpointAnnotation]:
  - breaking: true
    message: 'Illegal endpoint reference: The reference to the endpoint is not valid.'
    affected-element:
      type: Endpoint
      id: saveBillingAddressUsingPOST
```

The violation fits to the API changes reported before, which told us that the *saveBillingAddressUsingPOST* has been removed. Hence, we need to adjust the annotation model. We can do this by going over the list of API changes and violations and by removing and adding new appropriate elements to the annotation. For this demo, we provide an adjusted version of the annotation at ```solutions/v2/annotation-heat-clinic.yml```, which you can copy to ```cli-wd```, overwriting the old version of the file.

Finally, the new IDPA needs to be uploaded again:
```
app upload
ann upload
```

***[Continue with the next step...](6_load_test.md)***