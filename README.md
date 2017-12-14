# Continuous Maven Plugin

Continuous Integration / Continuous Delivery (Deployment) systems have
traditionally been hosted on dedicated servers in a stand-alone fashion (such
as Jenkins) or as part of an SCM system (such as Gitlab-CI).  With the adoption
of containers and container orchestration, it should no longer be necessary to
dedicate resources to a CI/CD system that runs constantly.  Since the load is
rarely constant, it should be much more effective to spin up a docker container
for each job that needs to be executed.  Parallel execution would be possible
simply by increasing the number of Maven jobs running in Docker containers.

---

** This plugin is experimental **

---

The goal of this plugin is to provide a means of "chaining" Maven builds, with
the "pipeline" steps being differentiated by Maven profiles.  Each profile
should therefore explicitly define the goals that are to be executed by that
step.  The following Maven command will start the build pipeline using the
main Maven configuration as the first step of the build:

```
mvn continuous:build
```

Each profile must define the prerequisite steps - Ordering the steps by number
allows only sequential ordering while defining the pipeline by defining the
next steps to be executed allows easy splitting but makes it harder to define
merge behavior.

To aid with building pipelines within Maven profiles and correctly defining the
predecessor steps, this plugin also provides a goal that displays a graph of
the entire pipeline.  Use the following command to view the pipeline's graph:

```
mvn continuous:graph
```

## Questions to be answered

During the experimental phase of this project, the following questions will be
explored:

1.  What's the best way to define the pipeline steps?
2.  Where should the build status be stored?
3.  Where should the build history be stored?
4.  Can SCM systems trigger the build process easily?
5.  How do we control resource usage/limits if jobs are independent?
