[![DOI](https://zenodo.org/badge/182383113.svg)](https://zenodo.org/badge/latestdoi/182383113)

# Demo of the Input Data and Properties Annotation

This demo presents how our approach to automated parameterization of load tests under evolving workloads and APIs can be used. We utilize Input Data and Properties Annotations (IDPAs) to parameterize generated load tests and evolve them over API changes.
The approach is implemented as part of [ContinuITy](https://github.com/ContinuITy-Project/ContinuITy).
As exemplary application to be load tested, we utilize the [Broadleaf Heat Clinic](https://github.com/BroadleafCommerce/DemoSite).

All steps can be replayed with the tooling provided in this repository. You are welcome to try it yourself. However, we also provide the results of all steps for an overview.

For cloning the repository to your local computer, please install [Git Large File Storage](https://git-lfs.github.com/) and use the following command:
```
git clone https://github.com/ContinuITy-Project/idpa-demo.git
```

## Content

The demo consists of the following steps:

0. [Reprequisites](instructions/0_prerequisites.md)
1. [Generating an Application Model](instructions/1_application_model.md)
2. [Annotating the Application Model](instructions/2_annotation.md)
3. [Extending to Full IDPA](instructions/3_full_idpa.md)
4. [Generating a Parameterized Load Test](instructions/4_load_test.md)
5. [Evolving the IDPA over API changes](instructions/5_evolution.md)
6. [Generating a Parameterized Load Test for the new API Version](instructions/6_load_test.md)

***[Start with the Demo...](instructions/0_prerequisites.md)***
