*[Back to contents](../README.md)*

## 6. Generating a Parameterized Load Test for the new API Version

At this point, we are ready for generating load tests for the new API version. As before, we need to do the following:

1. Switch the CLI context: ```order```

2. Create a new order with ```create``` and fill it with the following. This time, we need to base on session logs that fit to the new API version (```_persisted_2-heat-clinic```).

```yaml
---
goal: create-load-test
mode: past-sessions
tag: heat-clinic
options:
  duration: 60
  rampup: 1
  workload-model-type: wessbas
  load-test-type: jmeter
source:
  session-logs:
    link: session-logs/sessions/_persisted_2-heat-clinic
```

3. Submit the order with ```submit``` and wait for the result using ```wait 10000```. The output should look similar to the first test generation:

```yaml
---
order-id: heat-clinic-2
number: 1
max: 1
successful: true
created-artifacts:
  session-logs:
    link: http://localhost:8080/sessions/_persisted_2-heat-clinic
  workload-model:
    type: wessbas
    link: http://localhost:8080/workloadmodel/wessbas/model/heat-clinic-2
  load-test:
    type: jmeter
    link: http://localhost:8080/loadtest/jmeter/test/heat-clinic-2
  sessions-bundles:
    status: changed
internal-artifacts:
  tag: heat-clinic
  session-logs:
    link: session-logs/sessions/_persisted_2-heat-clinic
  workload-model:
    type: wessbas
    link: wessbas/model/heat-clinic-2
    jmeter-link: wessbas/jmeter/heat-clinic-2
    behavior-link: wessbas/behavior/heat-clinic-2
    application-link: wessbas/model/heat-clinic-2/application
    initial-annotation-link: wessbas/model/heat-clinic-2/annotation
  load-test:
    type: jmeter
    link: jmeter/loadtest/heat-clinic-2
  sessions-bundles:
    status: changed
```

4. Finally, you can download the created load test with
```
jmeter download http://localhost:8080/loadtest/jmeter/test/heat-clinic-2
```

We hope you enjoyed this demo and we could give you an impression how IDPAs are used in practice. If you are having issues with this demo or questions how to use IDPAs in another context, please [open an issue](https://github.com/ContinuITy-Project/idpa-demo/issues) and let us know.