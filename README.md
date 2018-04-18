Useful information about Google Cloud Products and Services.

- [Containers](https://cloud.google.com/containers/) - Overview
- [map-aws-google-cloud-platform](https://cloud.google.com/free/docs/map-aws-google-cloud-platform)
- [Compare Google to AWS](https://cloud.google.com/docs/compare/aws/)
- [Medium Article](https://medium.com/@robaboukhalil/a-tale-of-two-clouds-amazon-vs-google-4f2520516a38) - Google pricing is simpler and can be cheaper. Google has more configuration options for VMs. Google UX is better ("gone are the days of region-specific dashboard")
- [Migrate to Google Cloud](https://cloud.google.com/free/docs/frequently-asked-questions#migrating)

# Distinction between AppEngine and Firebase

https://medium.com/the-infinite-machine/app-engine-vs-firebase-welcome-to-bizzaro-world-24c257ef4908

https://stackoverflow.com/questions/37471546/google-app-engine-vs-firebase

https://cloud.google.com/solutions/mobile/mobile-app-backend-services
https://cloud.google.com/solutions/mobile/mobile-app-backend-services#design-pattern

https://www.quora.com/What-is-the-difference-between-Google-App-Engine-Firebase-and-Google-Endpoints

https://cloud.google.com/solutions/mobile/mobile-firebase-app-engine-flexible

# Products and Services

[Complete List of Services](https://cloud.google.com/terms/services)

[Products](https://cloud.google.com/products/)

## [Cloud Shell](https://cloud.google.com/shell/)

Google Cloud Shell provides you with command-line access to your cloud resources directly from your browser. You can easily manage your projects and resources without having to install the Google Cloud SDK or other tools on your system. With Cloud Shell, the Cloud SDK gcloud command-line tool and other utilities you need are always available, up to date and fully authenticated when you need them.

## [Stackdriver](https://cloud.google.com/stackdriver/)

Google Stackdriver provides powerful monitoring, logging, and diagnostics. It equips you with insight into the health, performance, and availability of cloud-powered applications, enabling you to find and fix issues faster. It is natively integrated with Google Cloud Platform, Amazon Web Services, and popular open source packages. Stackdriver provides a wide variety of metrics, dashboards, alerting, log management, reporting, and tracing capabilities.

## [Google Deployment Manager](https://cloud.google.com/deployment-manager/)

Google Cloud Deployment Manager allows you to specify all the resources needed for your application in a declarative format using yaml. You can also use Python or Jinja2 templates to parameterize the configuration and allow reuse of common deployment paradigms such as a load balanced, auto-scaled instance group. Treat your configuration as code and perform repeatable deployments.

[Supported Resource Types](https://cloud.google.com/deployment-manager/docs/configuration/supported-resource-types)

## [Container Builder](https://cloud.google.com/container-builder/)

Google Cloud Container Builder is a service that executes your builds on Google Cloud Platform infrastructure. Container Builder can import source code from Google Cloud Storage, Cloud Source Repositories, GitHub, or Bitbucket, execute a build to your specifications, and produce artifacts such as Docker containers or Java archives.

- Set up build triggers to automatically run new builds on every source code or tag change in your repository. Use custom build steps to run tests, export artifacts to Google Cloud Storage, and automate your software release process.
- Container Builder executes your build by running commands in a Docker container. Use our officially supported build steps, bring your own tooling, or use popular public Docker repositories like Maven and Gradle. If you can package it into a Docker container image, you can execute it as a step in your build process.

[Building, Testing, and Deploying Artifacts](https://cloud.google.com/container-builder/docs/configuring-builds/build-test-deploy-artifacts)

[Cloud Builders](https://cloud.google.com/container-builder/docs/cloud-builders)

**Build triggered from GitHub**
The following config shows a simple build that is triggered from GitHub. This type of configuration is typically used in a CI/CD pipeline.
In this example:

- The npm build step is called to install the dependencies and run unit tests.
- The docker build step is called to build a Docker image of the application and push the image to Container Registry.
- The kubectl build step is called to deploy the built image to the Kubernetes cluster.

```yaml
steps:
- name: 'gcr.io/cloud-builders/npm'
  args: ['install']
- name: 'gcr.io/cloud-builders/npm'
  args: ['test']
- name: 'gcr.io/cloud-builders/docker'
  args: ["build", "-t", "gcr.io/my-project/my-image:$REVISION_ID", "."]
- name: 'gcr.io/cloud-builders/docker'
  args: ["push", "gcr.io/my-project/my-image:$REVISION_ID"]
- name: 'gcr.io/cloud-builders/kubectl'
  args:
  - 'set'
  - 'image'
  - 'deployment/my-deployment'
  - 'my-container=gcr.io/my-project/my-image:$REVISION_ID'
  env:
  - 'CLOUDSDK_COMPUTE_ZONE=us-east4-b'
  - 'CLOUDSDK_CONTAINER_CLUSTER=my-cluster'
```

## [Google Transparency](https://cloud.google.com/access-transparency/)

Access Transparency gives you near real-time logs when Google Cloud Platform administrators access your content.

## [Compute Engine](https://cloud.google.com/compute/)

**Scalable, High-Performance Virtual Machines**

```
gcloud compute instances \
create my-vm \
--custom-cpu 4 --custom-memory 5
```

- All data written to persistent disk in Compute Engine is encrypted on the fly and then transmitted and stored in encrypted form. Google Compute Engine has completed ISO 27001, SSAE-16, SOC 1, SOC 2, and SOC 3 certifications, demonstrating our commitment to information security.
- With Sustained Use Discounts, we automatically give you discounted prices for long-running workloads with no sign-up fees or up-front commitment.
- With Committed Use Discounts you can save up to 57% with no upfront costs or instance-type lockin.

## [App Engine](https://cloud.google.com/appengine/)

**Build scalable web and mobile backends in any language on Google’s infrastructure**

- Supply your own Docker image or bring your own custom software stack, from language runtimes to frameworks to third party libraries.
- Offload infrastructure concerns like scaling your app up or down to handle traffic, load balancing, health-checking and healing your instances, and applying updates to the underlying OS
- Build your application in Node.js, Java, Ruby, C#, Go, Python, or PHP—or bring your own language runtime
- Google Stackdriver gives you powerful application diagnostics to debug and monitor the health and performance of your app
- Easily host different versions of your app, easily create development, test, staging, and production environments
- Route incoming requests to different app versions, A/B test and do incremental feature rollouts
- Help safeguard your application by defining access rules with App Engine firewall and leverage managed SSL/TLS certificates* by default on your custom domain at no additional cost

[Security Scanner](https://cloud.google.com/security-scanner/) - Cloud Security Scanner is a web security scanner for common vulnerabilities in Google App Engine applications. It can automatically scan and detect four common vulnerabilities, including:

- cross-site-scripting (XSS),
- Flash injection,
- mixed content (HTTP in HTTPS),
- and outdated/insecure libraries.

### Other features:

One command deployments:
```
gcloud app deploy
```

Local development environment (operates just like the Google App Engine but on your own machine for fast feedback during development):

```
dev_appserver.py --host 0.0.0.0 --admin_host 0.0.0.0 --port=8080 app.yaml --enable_sendmail
```

Cron Jobs:

```yaml
cron:
- description: script to check things every hour
  url: /crons/check
  schedule: every 1 hours
```

One config file to define basic project requirements:

```yaml
runtime: python27
api_version: 1
threadsafe: true

handlers:

- url: /css
  static_dir: static/css
- url: /img
  static_dir: static/img
- url: /js
  static_dir: static/js

- url: /foo
  script: python.foo.app
- url: /foo/(.*)
  script: python.foo.app

- url: /.*
  script: python.main.app

libraries:
- name: jinja2
  version: 2.6

skip_files:
- ^(.*/)?.*\.py[co]$

```

## [kubernetes](https://cloud.google.com/kubernetes-engine/)

**Deploy, manage, and scale containerized applications on Kubernetes, powered by Google Cloud**

managed environment for deploying containerized applications

Create cluster, scale it, deploy and update app.
```
gcloud container clusters create k0
kubectl run app --image gcr.io/google-samples/hello-app:1.0
kubectl scale deployment app --replicas 3
kubectl expose deployment app --port 80 --type=LoadBalancer
kubectl get service app
curl http://192.0.2.92:80
kubectl set image deployment app app=gcr.io/google-samples/hello-app:2.0
```

## [Cloud Functions](https://cloud.google.com/functions/)

Node.js (only official runtime), but you can [Extend runtime to go](https://github.com/GoogleCloudPlatform/cloud-functions-go) ... and it would make sense that Python/Java would be next.

max execution time: 540 seconds (9 mins) ... double AWS Lambda

[Compare Goolge and AWS](https://cloudacademy.com/blog/google-cloud-functions-serverless/)
Dependency management and deployment for AWS Lambda is difficult. In practice, you can use external dependencies only by including them within your zipped source code, and I find this inconvenient for many reasons.

- First, you are forced to compile and install these external packages on the same OS used by AWS Lambda internally. After this, every time you need to change something in your own code, you have to upload it all together.
- Second, this is not the way modern dependency management works. Web developers are now used to declaring and versioning their code dependencies, rather than providing local compiled libraries.

In fact, Google Cloud Functions allows you to define a simple package.json file to declare and version your npm dependencies

## [Cloud Vision API](https://cloud.google.com/vision/)

[Sensitive Data](https://cloud.google.com/solutions/sensitive-data-and-ml-datasets)

For images, you can use a text-detection service such as the Cloud Vision API to yield raw text from the image and isolate the location of that text within the image. The Vision API can provide the coordinates for locations of some targeted items within images, and you might use this information for example, to mask all faces from images of a cash register line before training a machine learning model to estimate average customer wait times.


## [Translate](https://cloud.google.com/translate/)

**Dynamically translate between thousands of available language pairs**

## [CLOUD DATA LOSS PREVENTION API](https://cloud.google.com/dlp/)

Automatically discover and redact sensitive data everywhere

The DLP API helps you better understand and manage sensitive data. It provides fast, scalable classification and redaction for sensitive data elements like credit card numbers, names, social security numbers, US and selected international identifier numbers, phone numbers and GCP credentials. The API classifies this data using more than 70 predefined detectors to identify patterns, formats, and checksums, and even understands contextual clues. You can optionally redact data as well using techniques like masking, secure hashing, bucketing, and format-preserving encryption.

## [Datastore](https://cloud.google.com/datastore/)

Cloud Datastore is a highly-scalable NoSQL database for your applications. Cloud Datastore automatically handles sharding and replication, providing you with a highly available and durable database that scales automatically to handle your applications' load. Cloud Datastore provides a myriad of capabilities such as ACID transactions, SQL-like queries, indexes and much more.

# Best Practice

[Best Practice Enterprise](https://cloud.google.com/docs/enterprise/best-practices-for-enterprise-organizations)

Google organizes your bill, including the exportable CSV or JSON version, by project. The project forms the top-level grouping of your invoice.

Cross-project access is possible but must be explicitly allowed

Implement SSO with SAML exchange

Use Cloud VPN to securely connect remote networks [Google Cloud VPN](https://cloud.google.com/vpn/docs/)

[CLOUD SECURITY SCANNER](https://cloud.google.com/security-scanner/) - Automatically scan your App Engine apps for common vulnerabilities

Cloud Router can add routes dynamically to Cloud VPN

Use Cloud Logging as a centralized location for logs [Stackdriver Logging Documentation](https://cloud.google.com/logging/docs/)

Cloud Storage automatically encrypts all data before it is written to disk

[Google Support](https://cloud.google.com/support/)
