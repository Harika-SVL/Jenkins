## Normal workflow for application deployments in Organisations

* There are 3 major workflow's in which projects fit-in :

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

## Our working with the pipelines

![Alt text](shots/1.PNG)

=> Step's we follow for any type (.net, java, sap) of application :

* Build the code
* Getting the package
* Creating an environment or deploying application into a existing service
* To automate this flow we use Jenkins

## Deployment options we choose

![Alt text](shots/2.PNG)

* In real every CI/CD tool is a CRON Job ( Scheduler ) on steroids ( can work over the failed cases also )

    * PaaS - Platform as a Service
    * IaaS - Infrastructure as a Service
    * SaaS - Software as a Service

## Proceeding with Jenkins

![Alt text](shots/3.PNG)

* Learning GIT ( Version Control System ) - Taking latest version of the code
* Sonar Qube ( Static Code Analysis ) - check for code written as per standards or not
* Jfrog/Artifactory ( Artifact Repository) - supports all the languages like storing java packages,linux packages,.net packages,Docker packages,etc - they also have artifactory scan features too
* Maven, MsBuild ( build java,.net applications) - to understand certain terms,dependencies,packaging phase,compiling phase

* Pipelines ( creating pipelines for applications) - two types
  1. UI oriented - Free style
  2. Pipeline as code - Declarative pipelines

* Administrative features :
  1. Backup
  2. Plugins
  3. User Management
  4. Multi nodes

## Maven installation 

* For java projects to work we need maven and java jdk to be present.
* Maven requires Java to be installed.

=> Distributions:
     * OpenJDK
     * Oracle JDK
     * IBM JDK
     * Amazon Corretto JDK

=> Versions:
     * 8
     * 11
     * 17
     * 19

=> Environmental Variables:
   * PATH : defines the which folder to be referred when a command is given (/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin)
   * JAVA_HOME : Directory where java gets installed (/usr/lib/jvm/java-8-openjdk-amd64)
   * M2_HOME : Directory where maven gets installed

[ We do these installations over Linux machine ]

## Java Installation
   ( openjdk-8 version)

=> Installation steps :

![Alt text](shots/4.PNG)

![Alt text](shots/5.PNG)

=> To add our own Environmental variables :

  1. For all the environments : vi /etc/environment

![Alt text](shots/6.PNG)

![Alt text](shots/7.PNG)

  2. For only our user : vi ~./bash

![Alt text](shots/8.PNG)

![Alt text](shots/9.PNG)

## Maven Installation

=> Installation steps :

![Alt text](shots/10.PNG)

![Alt text](shots/11.PNG)

## Sample : Building Game of life using maven
           ( This requires jdk-8 )

* Game of life repo : https://github.com/wakaleo/game-of-life

* To validate the pom.xml files created - 'mvn validate'

![Alt text](shots/12.PNG)
![Alt text](shots/13.PNG)

=> Commands to proceed through the workflow (life-cycle) : 

* Compile the code: 'mvn compile'

![Alt text](shots/14.PNG)
![Alt text](shots/15.PNG)

* Run the automated tests: 'mvn test'

![Alt text](shots/16.PNG)
![Alt text](shots/17.PNG)
![Alt text](shots/18.PNG)

* Create the package: 'mvn package'

![Alt text](shots/19.PNG)
![Alt text](shots/20.PNG)
![Alt text](shots/21.PNG)

=> History of all commands used :

![Alt text](shots/22.PNG)

## Sample : Building Spring-pet clinic using maven
       ( This requires jdk-17 )

![Alt text](shots/23.PNG)
![Alt text](shots/24.PNG)

* Setting variables and generating java-17

![Alt text](shots/25.PNG)
![Alt text](shots/26.PNG)

* Here if we want to permanently change the variables and path we go into bashrc and set the values
* Instead we can set temporarily using export command and setting variables and path for java-17 (as required)

![Alt text](shots/27.PNG)

* Spring-pet clinic repo : https://github.com/spring-projects/spring-petclinic

=> Commands to proceed through the workflow : 

* Compile the code: 'mvn compile'
* Run the automated tests: 'mvn test'
* Create the package: 'mvn package'

![Alt text](shots/28.PNG)

=>  Maven will download all the necessary dependencies to compile/package/test from a maven central repository ( https://mvnrepository.com/repos/central ) 

=> It downloads to M2_HOME which is by default '< HOME-DIR >/.m2' which is referred as local repository

## Maven Lifecycle Phases

    * Compile : Creates .class files
    * Test: Runs unit tests
    * Package: Create packages (jar/war)
    * Install: Copies the project which you have build to the local repository
 => Along with jar/war files as pom also gets copied


 # Jenkins

* Jenkins is an open source CI/CD Engine.
* Jenkins can be installed in following ways:
  * Using Package managers on Linux
  * Docker
  * Windows
  * WAR
* Official website for jenkins installation (here we can choose the method for installation) : https://www.jenkins.io/doc/book/installing/
* we would rather install LTS (Long Term Support Version) 
* For now we let's do it on ubuntu amchine : 

## Installing Steps for Jenkins :

=> For installing Jenkins we need to have java first ( openjdk-11-jdk)
* sudo apt update
* sudo apt install openjdk-11-jdk -y

![Alt text](shots/29.PNG)

[ From jenkins website installing steps ]
* curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
* echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
* sudo apt-get update
* sudo apt-get install jenkins -y

![Alt text](shots/29.PNG)

* After installing jenkins a user jenkins got created with

=> '/var/lib/jenkins' as Home directory

=> /bin/bash as default shell

* Also check if the user jenkins is created or not using ' cat /etc/passwd '

![Alt text](shots/30.PNG)

* Check for status of Jenkins :
  sudo systemctl start jenkins
  sudo systemctl status jenkins

![Alt text](shots/31.PNG)
![Alt text](shots/32.PNG)

* Now exposing it externally using < http://< Public_IP >:8080 > :

![Alt text](shots/33.PNG)
![Alt text](shots/34.PNG)

* After installing the suggested pluggins, create a admin user :

![Alt text](shots/35.PNG)
![Alt text](shots/36.PNG)

user : jenkinsuser
pass : jenkinsuser

* Jenkins homepage :

![Alt text](shots/37.PNG)

## Jenkins Projects

* They are of 3 types (majorly) : 
     1. Free Style: These projects are UI Based.
     2. Scripted Pipeline
     3. Declarative Pipeline

## Sample : Setting up a project (Job) to display system information )

* Lets create a Jenkins project which displays
  1. username
  2. current working directory
  3. all the environmental variables

* Lets start by create a Jenkins project (Freestyle), by clicking on 'New item'

![Alt text](shots/38.PNG)

* Now navigate to 'Build Steps' and select 'Execute shell'

![Alt text](shots/39.PNG)

* Now change the invoke shell steps to something as shown below

![Alt text](shots/40.PNG)

* Build the jenkins job

![Alt text](shots/41.PNG)

* Click on 'Build Now'

![Alt text](shots/42.PNG)
![Alt text](shots/43.PNG)

* Now select the console output

![Alt text](shots/44.PNG)

## Let also see a failure scenerio

* Edit the commands in the 'Build Steps' - shell prompt

![Alt text](shots/45.PNG)
![Alt text](shots/46.PNG)

* After changing and building again we get 

![Alt text](shots/47.PNG)
![Alt text](shots/48.PNG)

## Sample : Creating a project to run spring-pet clinic

* Manual steps : 
    * git clone https://github.com/spring-projects/spring-petclinic.git
    * cd spring-petclinic
    * mvn package
=> Doesn't get exposed over the browser

* Create a Jenkins job with name spc and in build steps invoke shell and execute
    * Complete installation of java-11 and jenkins on an ubuntu machine

![Alt text](shots/49.PNG)
![Alt text](shots/50.PNG)


![Alt text](shots/51.PNG)

* Install maven 


![Alt text](shots/52.PNG)
![Alt text](shots/53.PNG)
![Alt text](shots/54.PNG)

* Now rerun the same job

![Alt text](shots/55.PNG)

[spring-pet clinic doesn't work manually nor over jenkins job]

## Sample : Creating a project to run Game-of-life

* we install jenkins along with both java-8 (for Game-of-life)and java-17 (for java to be present)

![Alt text](shots/56.PNG)

* Complete installing jenkins

![Alt text](shots/57.PNG)

* Start working creating project and the Shell Script to be given is :

  *  export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH"
  * java -version
  * mvn --version
  * git clone https://github.com/wakaleo/game-of-life
  * cd game-of-life
  * mvn package

![Alt text](shots/58.PNG)

* Proceed and check  for the output :

![Alt text](shots/59.PNG)
![Alt text](shots/60.PNG)
![Alt text](shots/61.PNG)

## Create a new project for Game-of-life (over the UI selection options instead of the manual steps)

* Install jenkins on an ubuntu machine along with java-8 and java-17

![Alt text](shots/66.PNG)
![Alt text](shots/67.PNG)

* Setting different java or other tools

=> On the jenkins dashboard

Manage Jenkins => Tools => JDK => Add JDK

![Alt text](shots/63.PNG)

* Add any no.of versions that we need

=> give the name and home directory for java-17 and java-8 (using the export command on UI)

![Alt text](shots/64.PNG)
![Alt text](shots/65.PNG)

* Install maven 'sudo apt install maven -y' and check with the version

![Alt text](shots/68.PNG)
![Alt text](shots/69.PNG)

=> On the jenkins dashboard

Manage Jenkins => Tools => Maven => Add Maven

![Alt text](shots/70.PNG)
![Alt text](shots/71.PNG)

* Create a freestyle project to build game-of-life

=> On the jenkins dashboard

New item => gol => freestyle project => ok

![Alt text](shots/72.PNG)

## Exploring the options on dashboard

* General :-> general information about build project

![Alt text](shots/73.PNG)

* Source code management :-> about the version control information of the project

=> Add the REPO-URL and BRANCH-NAME and save

![Alt text](shots/74.PNG)

[only when Git is the public repo for opensource project,credentials are given for any other private repo for any project]

* As a root user ,Swith to jenkins user,go to home directory of jenkins 'JENKINS_HOME : var/lib/jenkins'

![Alt text](shots/75.PNG)
![Alt text](shots/76.PNG)

=> Every detail we mention in UI gets stored into config.xml file 'cat jobs/< project-name >/config.xml'

![Alt text](shots/77.PNG)

[No two projects can have same name]

=> Now build the project and let's explore workspace

![Alt text](shots/78.PNG)
![Alt text](shots/79.PNG)
![Alt text](shots/80.PNG)

=> Go back to gol => configure => Build steps => shell ( pwd ) => save

![Alt text](shots/81.PNG)
![Alt text](shots/82.PNG)

* Build Triggers : when to build - job to be called

![Alt text](shots/83.PNG)

* Build Environment : what to be built in the project

![Alt text](shots/84.PNG)

* Build steps : what to be done before building the project (there are many options)

![Alt text](shots/85.PNG)

* Post Build Actions : what to be done after build in the project

=> Sending email,
=> Setting GitHub status, etc

![Alt text](shots/86.PNG)

* Let's build game-of-life

=> General => JAVA_8_UBUNTU 

![Alt text](shots/87.PNG)

=> Source code management => git-url of gol

![Alt text](shots/88.PNG)

=> Build Environment => Delete workspace

![Alt text](shots/89.PNG)

=> Build steps => invoke top-level maven => package => save

![Alt text](shots/90.PNG)

=> Build now

![Alt text](shots/91.PNG)

[ If the working is delayed, we can resize the machine only after stopping the machine and restarting it again ]

 * To backup or preserve data of the project
 => we take the backup of '/var/lib/jenkins' folder frequently

* When we run the project we also get unit test results

=> Dashboard => click on the project

![Alt text](shots/94.PNG)
![Alt text](shots/95.PNG)

* Let's further configure some sections

=> Configue => Post build Actoins => Publish Junit test result report

![Alt text](shots/96.PNG)

=> For test report xml '**/surefire-reports/TEST-*.xml' 

![Alt text](shots/97.PNG)

=> Build now => console output

![Alt text](shots/98.PNG)
![Alt text](shots/99.PNG)
![Alt text](shots/100.PNG)

=> To show the results and artifact made directly

=>Dashboard => gol => Configure => Post-build Actions -> Archive the artifacts 

![Alt text](shots/101.PNG)

-> Files to archive - '**/target/gameoflife.war'

![Alt text](shots/102.PNG)

=> Save => build now

![Alt text](shots/103.PNG)
![Alt text](shots/104.PNG)

[After every change you make inorder to get the results, we need to build again and again]

## Plug-In in Jenkins

* It is an additional functionality provided , which will add functionality to Jenkins not to the machine(Virtual Machines) which we run 
( not an installation on the 'Jenkins master node' )

=> Dashboard => Manage Jenkins => Plugins => Installed plugins
=> Available plugins => search for the required plugins

![Alt text](shots/92.PNG)
![Alt text](shots/93.PNG)

## Build Excecutors (Build Executor Status)

* on Jenkins node determines how many projects can be built parallely

![Alt text](shots/105.PNG)

* An individual project by default gets only one executor, if you want to change this (not a good idea), we can give the no.of builds we want 

=> Every node in Jenkins can be configured with no.of executors
=> Manage Jenkins => Nodes and Clouds => Built-in Node -> Configure -> Put no.of executors you require

![Alt text](shots/106.PNG)
![Alt text](shots/107.PNG)

[Defulat case (may not be true for every job,some need two cpu's instead): generally for every virtual CPU a job is assigned and run]

## Distributed Builds

* Jenkins has 2 types of nodes :
     1. Master node : On which we install jenkins
     2. Node : On which we run the job which matches the label definition
* Here, Jenkins distributes the job based on the label or os used

![Alt text](shots/62.PNG)

* Adding more nodes increases no.of executors which means we can build more projects
* And to make Jenkins highly vailable also we increase the no.of master nodes those share a same folder 'var/lib/jenkins' we store the behaviour of that node
* So if even one server goes down the other is stayed as backup with doing the same work 

## Let's add a node(linux-ubuntu) to the master node

* Create two vm's with same configurations
* Install Java and Jenkins on the master node

##  Multi node configuration

![Alt text](shots/62.PNG)

* Create two vm's with basic configuration and name them as master and Node

![Alt text](shots/108.PNG)

* Install java-17 and jenkins on Master & Install java-8, java-17 and maven on the Node

![Alt text](shots/109.PNG)
![Alt text](shots/110.PNG)

* login into Jekins and create credentials

=> Manage Jenkins => Credentials

![Alt text](shots/111.PNG)

=> global => Add credentials

![Alt text](shots/112.PNG)
![Alt text](shots/113.PNG)

=> Start adding credentials

![Alt text](shots/114.PNG)
![Alt text](shots/115.PNG)

* Now to add the key, copy the key content from terminal and add into the section along with begin and end & create

![Alt text](shots/117.PNG)
![Alt text](shots/118.PNG)

* It's created

![Alt text](shots/119.PNG)

=> Dashboard => Manage Jenkins => Nodes and clouds => New Node

![Alt text](shots/120.PNG)
![Alt text](shots/121.PNG)
![Alt text](shots/122.PNG)

* Copy the IP address of the node for host ( Private IP also works if both master and node in same network) and save

![Alt text](shots/123.PNG)
![Alt text](shots/124.PNG)

* Wait and check for node is launched by clicking on node and logs => Launch agent (keep node machine also connected)
* Now configure Game of life
* Add jdk-8 and jdk-17 and save 
* Create a freestyle project gol and ok
* Configure for project gol
* JDk-8 , now restrict project to run with label as given with Node 'MAVEN_JDK-8' and give 'github url' with branch name as 'Master'
* Give the build steps with goal-package and in post build actions- archive the artifacts '**/gameoflife.war'
* Publish Junit result '**/target/surefire-reports/TEST-*.xml' an save
=> dashboard => |> symbol to build
* You get the archive built

## Jenkins-2 ( Pipeline as Code )

* Pipeline as a code refers to creating CI/CD Pipeline in some file format and version control (generally closer to code)

* Jenkins 1 was predominantly UI oriented, where as in Jenkins 2 the concept of pipelines were introduced natively.

* Now we write our build steps in these pipelines and then version control.

* Jenkins has created 2 types of pipelines

    1. Scripted Pipeline:
        * This pipeline allows to use Groovy Language directly
        * This is a different approach
    2. Declarative Pipeline
        * This pipeline internally uses Groovy but we use Jenkins DSL (Domain Specific Language)
        * Similar for the benifit of classic jenkins users

## Groovy

* There are two popular Java Based Languages
    1. Scala (Big Data Purposes)
    2. Groovy (Scripting purposes)

## Build Gameoflife on node1 using Scripted pipeline (sp)

* Create a new project gol-sp of pipeline type

=> Configure => pipeline => wirte the below pipeline => Save

[ In order to get help with the pipeline to write , click on pipeline syntax below and generate the code required]

------- Jenkins file

node('MAVEN_JDK8')
{
    stage('vcs')
    {
        git 'https://github.com/wakaleo/game-of-life.git'
    }
    stage('build') 
    {
        sh 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH" && mvn package'

    }
    stage('postbuild')
    {
        archiveArtifacts artifacts: '**/target/gameoflife.war', followSymlinks: false
        junit '**/surefire-reports/TEST-*.xml'
    }
}
-------
=> Dashboard => build symbol at  the project => Stage view / Console output
=> Build now

## Build Gameoflife on node1 using Declarative pipeline (dp)

* Create a new project gol-dp of pipeline type

=> Configure => pipeline => wirte the below pipeline => Save

[ In order to get help with the pipeline to write , click on pipeline syntax below and generate the code required]

------- Jenkins file

pipeline {
    agent { label 'MAVEN_JDK8' }
    stages {
        stage('VCS') {
            steps {
                git 'https://github.com/wakaleo/game-of-life.git'
            }
        }
        stage('build') {
            steps {
                sh 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH" && mvn package'
            }
        }
    }

}

-------
=> Dashboard => build symbol at  the project => Stage view / Console output
=> Build now

## Pipeline as Code (PAC)

* Pipeline as a code allows us to define CI/CD in a text document in any version control system

* CI/CD Pipeline when expressed as PAC will be present in git.

* Jenkins has started supporting Pipelines with
    1. Scripted Pipelines
    2. Declartive Pipelines

### Scripted Pipelines

* A pipeline can be defined in any file but 'Jenkins file' is most widely used name.

* The structure of Pipeline in scripted is as shown below

![Alt text](shots/126.PNG)

* Jenkins will have a set of steps which will be part of default jenkins installation and rest of steps can be added to jenkins by installing plugins

* Jenkins Pipeline steps reference : https://www.jenkins.io/doc/pipeline/steps/

## Sample : scripted pipeline for game of life

* let's create a directory And clone the code from git into it 'git clone < project_url >'
=> Clone the code using git pipeline : https://www.jenkins.io/doc/pipeline/steps/git/#git-git

* Create a branch 'git checkout -b < branch-name >'
=> Switched to the new branch

* Open code ' code .' to write a pipeline
=> Create a file 'Jenkins-file'

* Jenkins-file
----------------
node('MAVEN_JDK8') {
    stage('version control') {
        git url: 'https://github.com/khajadevopsmarch23/game-of-life.git',
            branch: 'scripted'
    }
}
--------------------
* Make your Jenkins node up and add 'git add .' , commit 'git commit -m "Added changes"' , push 'git push origin < Branch-name >' 

* Create a New item/view 
=> Name => List view => Create => Apply => ok

* In new project
=> New item => Name => pipeline => ok
=> Pipeline => Select- script from SCM => git => repo url (git url) => branch (created branch name) => Save => Build now

* Go to dashboard and check for working - stage view

* Now to build the package
* Jenkins-file
-------------------------------
        git url: 'https://github.com/khajadevopsmarch23/game-of-life.git',
            branch: 'scripted'
    }
    stage('build the code') {
        sh 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH" && mvn package'
    }
    stage('archive the artifacts') {
        archiveArtifacts onlyIfSuccessful: true,
            artifacts: '**/target/gameoflife.war',
            allowEmptyArchive: false
    }
    stage('show the test results') {
        junit testResults: '**/surefire-reports/TEST-*.xml',
              allowEmptyResults: true
    }
}
------------------------------------
(March 3 2023)

## Declarative Pipelines

* Jenkins has a DSL (Domain Specific Language) for creating Declarative Pipeines

* Jenkins Pipeline Syntax : https://www.jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline

![Alt text](shots/127.PNG)

* 