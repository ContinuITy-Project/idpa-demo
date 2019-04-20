*[Back to contents](../README.md)*

## 0. Prerequisites

For executing the demo, you need an installation of [Java version 1.8 or higher](https://www.java.com/) and a [Docker](https://www.docker.com/get-started) installation. Furthermore, you need an editor of your choice for YAML (.yml) files.

Go to the folder where this document is placed and execute the following two commands:
1. Start our [ContinuITy](https://github.com/ContinuITy-Project/ContinuITy) tool, which implements the load test generation including parameterization with IDPAs: ```docker-compose up -d```
2. Start the ContinuITy CLI, which we will use to work with IDPAs locally and to interact with the ContinuITy tool:
    * ```sh startCli.sh``` for Linux/Mac
    * ```startCli.bat``` for Windows

We already preconfigured the CLI such that all created artifacts will be stored in ```cli-wd```.

***[Continue with the next step...](1_application_model.md)***