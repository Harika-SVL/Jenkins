## Normal workflow for application deployments in Organisations

* There are 3 major workflow's in which projects fit n :

   1. Virtual/Physical machine Deployment
   2. Infra Provisioning and Deployment
   3. Containerized Deployment

=>  Aplications are deployed on :

   1. Virtual machine/Physical machine :
         * OnPrem
         * Cloud
   2. Containers :
         * Docker
         * Kubernetes-k8s (OnPrem/Cloud)
   3. Cloud Native Applications :
        * PaaS (Azure-App Service/AWS-Elastic BeanStalk)
        * FaaS (Azure-Functions/AWS-Lamda)      

## Our Performing in the pipelines

![Alt text](shots/1.PNG)

=> Steps we follow for any type(.net,java,sap) of application :
* Build the code
* Getting the package
* Creating an environment or deploying application into a existing service
* To automate this flow we use Jenkins

## Deployment options we choose

![Alt text](shots/2.PNG)

* In real every CI/CD tool is a CRON Job ( Scheduler ) on steroids ( can work over the failed cases also )

=> PaaS - Platform as a Service
=> IaaS - Infrastructure as a Service
=> SaaS - Software as a Service

## Proceeding with Jenkins

![Alt text](shots/3.PNG)

* Learning GIT ( version control system ) - Taking latest version of the code
* Sonar Qube ( Static code analysis ) - check for code written as per standards or not
* Jfrog/Artifactory ( Artifat Repository) - supports all the languages like storing java packages,linux packages,.net packages,Docker packages,etc - they also have artifactory scan features too
* MAven,MsBuild ( build java,.net applications) - to understand certain terms,dependencies,packaging phase,compiling phase
* Pipelines ( creating pipelines for applications) - two types
  1. UI oriented - Free style
  2. Pipeline as code - Declarative pipelines
* Administrative features :
  1. Backup
  2. Plugins
  3. User Management
  4. Multi nodes

  