### Install-JENKINS

* [Refer Here : https://www.jenkins.io/doc/book/installing/linux/] for installing jenkins on linux
* Installing on Ubuntu-steps: 
    [Refer Here : https://www.jenkins.io/doc/book/installing/linux/#debianubuntu]
```
sudo apt update 
sudo apt install openjdk-17-jdk -y
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
```
* Navigate to `http://<public-ip>:8080`

![Alt text](shots/1.PNG)

* Find the initial Admin password
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
![Alt text](shots/2.PNG)
![Alt text](shots/3.PNG)

* Now install suggested plugins

![Alt text](shots/4.PNG)
![Alt text](shots/5.PNG)

* Create a new admin user

![Alt text](shots/6.PNG)
![Alt text](shots/7.PNG)
![Alt text](shots/8.PNG)
![Alt text](shots/9.PNG)

### CONTINUOUS INTEGRATION and CONTINUOUS DELIVERY/DEPLOYMENT

* To perform frequent integrations and deployments we need a tool which can help us doing the same stuff and integrate with multiple tools. These tools are generally called as `CI/CD Engines`
* Jenkins is popular Opensource CI/CD Engine
* Any CI/CD tool at it's core is a `CRON` on steroids

#### CRONJOB In Linux - CRONTAB (periodic tasks on steroids)
      [Refer Here : https://crontab.guru/]

* “cron” is a Linux-based utility used to schedule scripts or programs
* The `CRONTAB` is a list of commands that you want to run on a regular schedule, and also the name of the command used to manage that list. Crontab stands for “CRON TABLE”, because it uses the job scheduler cron to execute tasks
```
Syntax : <Minute> <Hour> <Day_of_the_Month> <Month_of_the_Year> <Day_of_the_Week> <command>
```
![Alt text](shots/12.PNG)
![Alt text](shots/13.PNG)

* Minute – value can be between 0-59
* Hour – value can be between 0-23
* Day_of_the_month – value can be between 1-31. For the months having fewer days will ignore remaining part
* Month_of_the_year – value can be between 1-12. You can also define this value with the first three alphabets of the month like jan, feb, mar, apr etc.
* Day_of_the_Week – value can be between 0-7. Where 0 and 7 for Sunday, 1 for Monday, 2 for Tuesday, and so on. You can also use the first three alphabets of days like sun, mon, tue, wed, etc.

#### CRONJOB In Windows - TASK SCHEDULER
       [Refer Here : https://linuxhint.com/set-up-cron-job-windows/]

* In Windows, it is mostly utilized to automate the update system and scheduled tasks that will run automatically without manual execution. 
* If you want to create a new task or cron job on Windows, perform the required operation with the help of the “TASK SCHEDULER”.

#### What happens when we install jenkins..?

* When we install jenkins we will have a default user created called as `JENKINS`
    * From jenkins we can perform anything which jenkins user performs

![Alt text](shots/10.PNG)

* How can we integrate jenkins with any other tools:
    * COMMAND LINE: call the command line
    * PLUGIN(Just gives an UI option to add in order to be converted to low level linux commands) + installation/configuration
      * UI or PIPELINE step

#### PATH variable 'echo $PATH'
      * To find path in linux 'whereis <needed-name>'
#### Environment Variable
      * Every process in the system have their own ID and CPU, here Environmental variable stays common for all the processes in a system
      * System environmental variable(available to all the users present in a system) 'sudo vi /etc/environment'
      * User environmental variable (available only to the specific user) 'home/bashrc'

#### NOTE:
      * Adding sudo permission to Linux user 
          [Refer Here: https://www.baeldung.com/linux/sudo-privileges-user]
```
sudo visudo

jenkins (ALL:ALL) NOPASSWD:ALL
```
#### COMPILER vs INTERPRITOR vs HYBRID based applications

* COMPILER-based application

  [Dubbing before running the application] 

![Alt text](shots/14.PNG)

* INTERPRETOR-based application

  [Translation during running of the application]

![Alt text](shots/15.PNG)

* HYBRID-based (both compiler and interpretor) application

  [Before running the application the compilation is done to Intermediate Language and then through the Interpretor coverts into server understandable]

![Alt text](shots/16.PNG)

![Alt text](shots/17.PNG)

### DEPENDENCIES

* Whenever a software project is developed, they have lot of dependencies
* Before building the code, dependencies have to be present locally
* To manage these dependencies, every programming language has some kind of package manager

[NOTE : Package Management is downloading the packages, building the packages and distributing the packages]

  * dotnet: `nuget` is the package manager
     * File to store the dependencies `packages.config/packages.json`
  * java: `maven` can handle package management
  * python: `pip` is the package manager
  * nodejs: `npm` can handle package management

### BUILD (every build) Workflow Structure

* Scope of Work :

![Alt text](shots/11.PNG)

## MAVEN

* Maven is a tool which can be used to build, package, distribute, test and generate documentation for java and java-based languages(groovy,scala)
* It follows convention(SNAPSHOT & RELEASE) over configuration
* It uses a file called as 'pom.xml' ( POM - Project Object Model )
* Apache Log4j Security Vulnerabilities

* ARTIFACTS (reasons) : 

=> To avoid the errors occuring freshly

=> To try to resolve the existing errors

### MAVEN Installation:

#### Install JAVA-17
```
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```
![Alt text](shots/18.PNG)

* Let's try installing MAVEN 3.9.3 

    [Refer Here: https://maven.apache.org/download.cgi]
```
cd /tmp/
wget https://dlcdn.apache.org/maven/maven-3/3.9.3/binaries/apache-maven-3.9.3-bin.tar.gz
sudo mkdir /usr/share/maven
sudo tar -xvzf apache-maven-3.9.3-bin.tar.gz -C /usr/share/maven
# add `/usr/share/maven/apache-maven-3.9.3/bin` to the PATH variable
# add to `~/.bashrc` or `/etc/environment`
cd ~
sudo vi /etc/environment
# exit and relogin
mvn --version
```
![Alt text](shots/19.PNG)
![Alt text](shots/20.PNG)
![Alt text](shots/21.PNG)
![Alt text](shots/22.PNG)
![Alt text](shots/23.PNG)

#### MAVEN GOALS and LIFECYCLE :
    [Refer Here : https://www.baeldung.com/maven-goals-phases]

* VALIDATE: validates the pom and it's project
* COMPILE: converts the java code into byte code (.java to .class). It stores the class files in `target/classes`
* TEST: will run the unit tests written and generates test results in xml format of text format. Folder will be `/target/surefire-reports/TEST-*.xml`

![Alt text](shots/42.PNG)

* PACKAGE: creates the packaging format (jar/war/ear) and will be `<artifact-id>-<version>.<packaging-format>`
* INSTALL: copies the package and it's definition into `M2_HOME` or `~/.m2/repository`
* DEPLOY: copying package and it's definition to remote repository for other users in other systems to use what you have built (This command is equivalent to git push command)
* CLEAN: removes target folder

=> Here, when we execute a goal, all the pevious goals also get's executed

##### LIFECYCLE 
 
       [Refer Here : https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Lifecycle_Reference]
* To execute any lifecycle goal `mvn <goal>`
* Simple POM file
```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>io.learningthoughts.samples</groupId>
  <artifactId>hello-maven</artifactId>
  <version>1.0.0-SNAPSHOT</version>
  <properties>
     <maven.compiler.source>11</maven.compiler.source>
     <maven.compiler.target>11</maven.compiler.target>
  </properties>
  <dependencies>
    <dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
   </dependency>
  </dependencies>
</project>
```
* Maven PACKAGING formats: 
    [Refer Here : https://www.baeldung.com maven-packaging-types#:~:text=Maven%20offers%20many%20default%20packaging%20types%20that%20include%20a%20jar,and%20performs%20a%20specific%20task.]
* Maven goals downloads dependencies and stores in
  * `M2_HOME` where ever this environment variable points to and if not found does in `<home-dir>/.m2`

  ### Exercise

* Try installing maven and create a simple jenkins project with following build steps:
```
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic 
mvn package
```
#### MANUAL STEPS :

##### Installing JAVA-17
```
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```
##### Installing MAVEN
```
cd /tmp/
wget https://dlcdn.apache.org/maven/maven-3/3.9.3/binaries/apache-maven-3.9.3-bin.tar.gz
sudo mkdir /usr/share/maven
sudo tar -xvzf apache-maven-3.9.3-bin.tar.gz -C /usr/share/maven
cd ~
sudo vi /etc/environment
# add '/usr/share/maven/apache-maven-3.9.3/bin'
exit
# relogin into the machine
mvn --version
```
##### Building SPRING-PETCLINIC
```
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic/
mvn package 
```
### TERMS

* ARTIFACT 

=> For generating artifacts we use build tools like msbuild, maven/gradle

=> These are referenced in a pipeline stage for automated deployment to the target environment

* UNIT TEST 

=> java-junit, microsoft-mstest/nunit, python-pytest, nodejs-jasmine, nodejs-mocha, most CI/CD systems understand junit xml reports to generate test results
            
=> incorporating unit testing into the DevOps process, which involves automating the entire software development life cycle to enable faster delivery of software while maintaining its quality

* CODE COVERAGE 

=> we do this from Sonar Qube

=> helps you determine the proportion of your project's code that is actually being tested by tests such as unit tests. To increase your confidence of the code changes, and guard effectively against bugs, your tests should exercise - or cover - a large proportion of your code

[ Code Coverage = Branch Coverage (testing method, which aims to ensure that each one of the possible branch from each decision point is executed at least once and thereby ensuring that all reachable code is executed) + Line Coverage (how many of lines of source code have been tested) ]

* STATIC CODE ANALYSIS 

=> we do this from Sonar Qube, figuring best code analysis

=> method of computer program debugging that is done by examining the code without executing the program. The process provides an understanding of the code structure and can help ensure that the code adheres to industry standards

* ARTIFACT REPOSITORY 

=> we would use jfrog (azure artifacts)

=> Artifacts are large binary packages that are created throughout the development and release process. An artifact repository is a software application designed to manage these artifacts

### Building Maven projects using Jenkins  

#### JENKINS CONFIGURATION

* Install jenkins (jdk-17)
* Install and configure maven in Jenkins (Master Node)

    * Start a vm

      ![Alt text](shots/24.PNG)

    * Install java-17

      ![Alt text](shots/25.PNG)

    * Install jenkins and configure as jenkins user

      ![Alt text](shots/26.PNG)

    * Add jenkins to sudoers   WORKSPACE: `/var/lib/jenkins`

      ![Alt text](shots/27.PNG)

    * Install maven as a root-jenkins user

      ![Alt text](shots/29.PNG)
    
* Let's build spring-petclinic 
    [Refer Here : https://github.com/spring-projects/spring-petclinic]

    * software requirements
      * jdk-17
      * maven

* Create a free style project to build spring-petclinic

=> New item => Freestyle project (name= spc-daybuild) => ok

![Alt text](shots/30.PNG)

* Free-style project sections

=> Description : This is to build spring-petclinic project 

1. GENERAL: This represents the project information
      
    ![Alt text](shots/31.PNG)

2. SOURCE CODE MANAGEMENT: This represent the code to be used for CI/CD pipelines

    ![Alt text](shots/32.PNG)

3. BUILD TRIGGERS: represents when to build

  * BUILD PERIODICALLY(CRON): If the project has to be built based on schedule, write cron expression into this 
                                [Refer Here : https://crontab.guru/]

  * POLL SCM: represents jenkins polling scm (asking git) and the cron expression represents how frequently it should ask. It is triggered only when there are changes in the code.

    ![Alt text](shots/33.PNG)

4. BUILD ENVIRONMENT: represents the environmental configuration

   ![Alt text](shots/34.PNG)

5. BUILD STEPS: actual activities that are performed during execution

   ![Alt text](shots/35.PNG)
   ![Alt text](shots/36.PNG)

6. POST BUILD ACTIONS: actions to be performed after completion of build

   ![Alt text](shots/37.PNG)
   ![Alt text](shots/38.PNG)

* Now we can wait for the trigger to call the job or trigger build manually

 ![Alt text](shots/39.PNG)
 ![Alt text](shots/40.PNG)

* In Jenkins we can have multiple versions of java, maven, etc and we can handle these by configuring jenkins
* To fix the maven 3.6.3, issue we have to install 3.9.4 and use full path for package
```
cd /tmp
wget https://dlcdn.apache.org/maven/maven-3/3.9.4/binaries/apache-maven-3.9.4-bin.tar.gz
sudo mkdir /usr/share/maven3.9
sudo tar -xvzf apache-maven-3.9.4-bin.tar.gz -C /usr/share/maven3.9
cd spring-petclinic/
/usr/share/maven3.9/apache-maven-3.9.4/bin/mvn package
```
* Go back and re-configure the maven version

![Alt text](shots/43.PNG)
![Alt text](shots/44.PNG)
![Alt text](shots/45.PNG)

* Test results

  ![Alt text](shots/46.PNG)
  ![Alt text](shots/41.PNG)
  ![Alt text](shots/42.PNG)

  ### Jenkins TERMS :

* JENKINS_HOME: Jenkins home is a folder where jenkins stores all of it's configuration. In the above case the workspace is `/var/lib/jenkins`. If you want to change the workspace deal with `JENKINS_HOME`

![Alt text](shots/28.PNG)

* Backup for Jenkins is backup of Workspace (/var/lib/jenkins)

* PROJECT: This contains the activity that needs to be performed on triggers
    * This project is stored as xml file in workspace
    * Types of projects :
      * Freestyle project: This is UI based configuration
      * Pipeline: This is instructions expressed in some code format (pipeline as a code)

* BUILD: This represents the execution of project. Every build for a project has a running number called as Build_id

* NODE: This represents the machine on which build can be executed. Each Node can be configured to handle multiple builds by executors(no.of parallel working projects)

### Managing DIFFERENT VERSIONS of the tools using jenkins

* Connect to the jenkins installed vm 

=> Manage jenkins => Tools => Maven installations

  ![Alt text](shots/47.PNG)
  ![Alt text](shots/48.PNG)

* Connect to the machine through command line
```
sudo -i
su jenkins
cd /usr/share/maven (maven 3.6.3)
ls
cd /usr/share/maven/apache-maven-3.9.4   (maven 3.9.4)
```
  ![Alt text](shots/49.PNG)

* Now lets configure the spring-petclinic to use top level maven targets

  ![Alt text](shots/50.PNG)

* Now build the project manually (Build Now)

  ![Alt text](shots/51.PNG)

### DISTRIBUTED BUILDS

* Setup:
  1. Fork Spring-petclinic   
      => spring-petclinic github => fork => owner,repo name => copy main branch only => create fork
      
      [Refer Here : https://github.com/Harika-SVL/spring-petclinic]

    * requirements to build
        * java jdk 17
        * maven 3.9

  2. Fork game of life 
      => game of life github => fork => owner,repo name => copy main branch only => create fork

      [Refer Here : https://github.com/Harika-SVL/game-of-life]
    
    * requirements to build
        * java 8
        * maven

  3. Fork nopcommerce
      => nopcommerce github => fork => owner,repo name => copy main branch only => create fork

      [Refer Here : https://github.com/Harika-SVL/nopCommerce]
     
    * requirements to build
        * dotnet 7

* To handle different builds with different software needs, we tend to use different servers.
* Jenkins has distributed builds where we can distribute the builds on differnt nodes by matching labels

* While creating a project we can set labels and expect them to be executed on the node matching labels

  ![Alt text](shots/53.PNG)

#### How to add MULTIPLE NODES to jenkins

* Let's create 2 ubuntu VM's and let's make one vm the jenkins-master
* On it install java-17,jenkins and configure jenkins and add the user to sudoers
```
sudo apt update
sudo apt install openjdk-17-jdk -y
```
##### NOTE
=> To install jenkins we can use the following script
```bash
#!/bin/bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install openjdk-17-jdk jenkins -y
```
  ![Alt text](shots/54.PNG)

* To check the sudoers
```
sudo -i
su jenkins
cd ~
sudo apt update
```
### Node 1 => JDK-17 and maven 3.9.4

* let's make other vm the node-1
* On this node (we will be using existing credentials) we will install java-17 and install maven 3.9.4
```
sudo apt update
sudo apt install openjdk-17-jdk -y
```
```
cd /tmp
wget https://dlcdn.apache.org/maven/maven-3/3.9.4/binaries/apache-maven-3.9.4-bin.tar.gz
sudo mkdir /usr/share/maven
sudo tar -xvzf apache-maven-3.9.4-bin.tar.gz -C /usr/share/maven
sudo vi /etc/environment
# add ':/usr/share/maven/apache-maven-3.9.4/bin'
exit
# relogin
mvn --version
```

  ![Alt text](shots/55.PNG)

* Now let's configure the jenkins-master node with label `JDK-17`
* On Jenkins UI Navigate to 

=> Manage Jenkins => Nodes and Clouds

  ![Alt text](shots/56.PNG)

=> New node => name: node-1 , select permanent agent => create

  ![Alt text](shots/57.PNG)

* Configuring the node-1 information

  ![Alt text](shots/58.PNG)
  ![Alt text](shots/59.PNG)

=> host : node private_ip (both in same network) => credentials : select jenkins => select kind and id

  ![Alt text](shots/60.PNG)

=> Add description, Username => select Enetr directly => add ssh-private key (cat id_rsa) => Add

  ![Alt text](shots/61.PNG)

=> Add Host, credentials, Host key => Save

  ![Alt text](shots/62.PNG)

* node-1 gets connected

  ![Alt text](shots/63.PNG)


#### Let's setup spring-petclinic to execute on node-1

* Configure spc-day build same as last session with one restriction in General section

* Start a new project

  ![Alt text](shots/64.PNG)

=> Select source code management => git : select new forked url, branch: main

  ![Alt text](shots/65.PNG)

=> Select Build Triggers => Poll SCM : * * * * *

  ![Alt text](shots/66.PNG)

=> selecct Build Steps => Invoke top-level maven targets => Goals : package => Save

  ![Alt text](shots/67.PNG)

=> go to configure again => select when to run => Add label => Save

  ![Alt text](shots/68.PNG)

* Now build and verify the console output

  ![Alt text](shots/69.PNG)
  ![Alt text](shots/70.PNG)
  ![Alt text](shots/71.PNG)

* Now let's add processing the test results `**/surefire-reports/TEST-*.xml`
* As a result of this project's build, I get `gameoflife.war` which is called as `ARTIFACT`. Let's configure jenkins to archive the artifacts

  ![Alt text](shots/87.PNG)
  ![Alt text](shots/88.PNG)

#### Exercises

* Create a jenkins master with t2.micro (ubuntu)
* Create a node with any other os redhat/centos/amazon linux
    * install jdk 17
* Create a job which should run on the other node configure and display its ip address and environmental variables printenv

### Node 2 => JDK-8 and maven

* On the jenkins-master we would require jdk-17 and for the project game-of-life we would require jdk-8
* On the node-2, let's create a new user called as devops and add to sudoers with `NOPASSWD`
```
sudo adduser devops
# password : devops
sudo visudo
# devops  ALL=(ALL:ALL) NOPASSWD:ALL
```
* Now enable password based authentication
```
sudo vi /etc/ssh/sshd_config
# Change password Authentication to yes
sudo systemctl restart sshd
```
* Restart as devops user
```
exit
ssh devops@<public_ip>
password : devops
```
* Install jdk-8, jdk-17 and maven
```
sudo apt update
sudo apt install openjdk-8-jdk openjdk-17-jdk -y
sudo apt install maven -y
```
* Now execute java -version

  ![Alt text](shots/72.PNG)

* Lets configure JDK-17 and JDK-8 paths in tools section of jenkins (jenkins-master)

  ![Alt text](shots/73.PNG)

* Now add node-2 to jenkins

  ![Alt text](shots/74.PNG)

=> Configuring credentials

  ![Alt text](shots/75.PNG)
  ![Alt text](shots/76.PNG)
  ![Alt text](shots/77.PNG)

* Now let's try building game of life

  ![Alt text](shots/78.PNG)
  ![Alt text](shots/79.PNG)
  ![Alt text](shots/80.PNG)

=> Build Now 

  ![Alt text](shots/81.PNG)

* Now let's add processing the test results `**/surefire-reports/TEST-*.xml`

  ![Alt text](shots/82.PNG)
  ![Alt text](shots/83.PNG)

=> Build Now

  ![Alt text](shots/84.PNG)

* As a result of this project's build, I get `gameoflife.war` which is called as `ARTIFACT`. Let's configure jenkins to archive the artifacts

  ![Alt text](shots/85.PNG)

=> Build Now

  ![Alt text](shots/86.PNG)

* Note: We have implemented the same for spring petclinic

  ![Alt text](shots/87.PNG)
  ![Alt text](shots/88.PNG)

* Note: The health of the builds is represented as weather in jenkins
    * cloudy means builds are failing
    * sunny means the builds are successful

  ![Alt text](shots/89.PNG)

### Node 3: Executing dotnet project on jenkins

* For agent we required jdk-17
* Create an ec2 instance (node-3)  with size 20 GB
* install dotnet-7 sdk for running nop comerce
* Installation instructions 
  [Refer Here : https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-2204]
```
sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-7.0
dotnet --help
```
  ![Alt text](shots/90.PNG)

* Configuring node-3 on dashboard

  ![Alt text](shots/91.PNG)
  ![Alt text](shots/92.PNG)

=> Install jdk-17 on the node

  ![Alt text](shots/93.PNG)
  ![Alt text](shots/94.PNG)

* to build the dotnet project we need to restore nuget packages
```
cd /tmp/
git clone https://github.com/Harika-SVL/nopCommerce.git
cd nopCommerce
git branch
# dotnet restore <path of project or sln>
dotnet restore src/NopCommerce.sln
# For night builds
# dotnet build  -c "Release" <path of project or sln> 
dotnet build -c Release src/NopCommerce.sln
# For day builds
# dotnet build  -c "Debug" <path of project or sln> 
```
### Upstream and Downstream projects

* If the Project A triggers the Project B then
    * Project B is downstream of Project A
    * Project A is upstream of Project B

  ![Alt text](shots/95.PNG)

* Create a new view Project A, Project B, Project C

  ![Alt text](shots/96.PNG)

=> New item => Project A => Freestyle Project => OK

=> Description : This is Project A => Buils steps : Execute shell - echo "Project A", sleep 10s => Save

  ![Alt text](shots/97.PNG)

* To connect the projects with each other

=> Project C => configure => Build Triggers => Build after other projects are build => Project B => save

  ![Alt text](shots/98.PNG)

OR

=> Project A => configure => Post-build Actions => Build other projects : Project B => Trigger only if build is stable => save

  ![Alt text](shots/99.PNG)

* Repeat above steps for Project B and Project C 

  ![Alt text](shots/100.PNG)
  ![Alt text](shots/101.PNG)
  ![Alt text](shots/102.PNG)

* Now build Project A and all the three projects get executed as they are connected and with a gap of 10sec each

  ![Alt text](shots/103.PNG)

### Parameterized Builds

* While building the jobs, sometimes we would like users to pass some information.This is called as parameters
* Create a new view with `list view` option

  ![Alt text](shots/104.PNG)

* Select the jobs- gameoflife, nopCommerce, spc-Day-build

  ![Alt text](shots/106.PNG)

* Now let's enable parameters for some jenkins(gameoflife) project/job

  ![Alt text](shots/107.PNG)
  ![Alt text](shots/108.PNG)

* Create some parameters and use it in the build steps

  ![Alt text](shots/109.PNG)
  ![Alt text](shots/110.PNG)

* Save and build the goal

  ![Alt text](shots/111.PNG)
  ![Alt text](shots/112.PNG)
  ![Alt text](shots/113.PNG)
  ![Alt text](shots/114.PNG)

### Jenkins Environmental variables

* Jenkins injects environmental variables into every job in addition to environmental variables present on node
* To view environmental variables, select any project and navigate to build steps => execute shell

  ![Alt text](shots/115.PNG)
  ![Alt text](shots/116.PNG)

* Doc's on environmental variables
    [Refer Here : https://www.jenkins.io/doc/book/pipeline/jenkinsfile/#using-environment-variables]

* Sample using environmetal variables (game of life on node-2 to print environmental variables)

=> Create new project 'Environmentalvariablesdemo' in 'Experimental' view => General : Jdk-JAVA_8, Restrict-JDK_8 => Build steps : Execute shell-printenv => Save => Build Now

* Result - Console Output

  ![Alt text](shots/117.PNG)

* Sample using Environmetal variables (Environmentalvariablesdemo)

=> Create new project 'Environmentalvariablesdemo' in 'Experimental' view => Build steps : Execute shell- echo "Hello, this project-url is ${JOB_DISPLAY_URL} and the build-id is ${BUILD_ID}", echo "Hello, this project is running in folder ${WORKSPACE} on NODE ${NODE_NAME}" => Save => Build Now

  ![Alt text](shots/118.PNG)

* Result - Console Output

  ![Alt text](shots/119.PNG)
  
### How to take backup of jenkins (backup of /var/lib/jenkins folder)

* One option for backup is configuration files

=> Manage Jenkins => plugins => Available plugins => search-backup => periodic backup

  ![Alt text](shots/120.PNG)
  ![Alt text](shots/121.PNG)

* To restart jenkins (only if you are admin)

=> refresh the page => relogin => In the url : `http://18.60.61.74:8080/restart`

* Configuring the frequency for backup

=> Manage Jenkins => Periodic backup manager => Configure

  ![Alt text](shots/122.PNG)
  ![Alt text](shots/123.PNG)
  ![Alt text](shots/124.PNG)
  ![Alt text](shots/125.PNG)

=> Save => Backup Now

  ![Alt text](shots/126.PNG)

  #### Which plugin should be installed to monitor jenkins ?

  [Refer Here : https://plugins.jenkins.io/monitoring/]

* Monitoring option

=> Dashboard => Manage Jenkins => plugins => Available jenkins => search : monitoring => select Monitoring => Install without restart => Restart jenkins when no jobs running

  ![Alt text](shots/128.PNG)

* Jenkins Plugins can be installed from
    * Market place
    * Uploading the plugin
* Jenkins plugin has two extensions
    * jpi (Jenkins plugin interface)
    * hpi (hudson plugin interface) (old)

#### Exercise

* Figure out a plugin to change Build_id
* Create a folder in '/tmp' of your node with project name
```
/tmp/gameoflife
```
* In this folder try to create one more folder with build-id
```
/tmp/gameoflife/5
```
* to this folder copy the war/jar file

### Pipeline as Code

* This is expressing CI/CD pipleine in terms of some code/expressions/statements
* This is part of version control i.e. each change done to the steps will have history
* Official docs [Refer Here : https://www.jenkins.io/doc/book/pipeline/pipeline-as-code/]

* Azure DevOps
```
# Starter pipeline
# Start with a minimal pipeline that you can customize to build and deploy your code.
# Add steps that build, run tests, deploy, and more:
# https://aka.ms/yaml

trigger:
- main

pool:
  name: Default
steps:
  - task: Maven@3
    inputs:
      mavenPOMFile: 'pom.xml'
      goals: 'package'
      publishJUnitResults: true
      testResultsFiles: '**/surefire-reports/TEST-*.xml'
      testRunTitle: 'unittests'
```
* Jenkins
```
node("JDK-11-MVN") {
  stage("get-code") {
    sh " git clone https://github.com/spring-projects/spring-petclinic.git && cd spring-petclinic"
  }
  stage("build") {
    sh "mvn package"
    junit '**/surefire-reports/TEST-*.xml'
  }
}
```
* The only manual work would be done is to, go to jenkins, create a pipeline project and configure where your pipeline is

### Pipeline as Code in Jenkins

* Jenkins has two flavours
    * Scripted Pipeline
        * Developed where you can execute groovy language directly
    * Declartive Pipeline
        * Jenkins has created a DSL (Domain specific Language) which is mostly inspired from traditional jenkins

#### Creating a Scripted Pipeline

* Create a game of life project (Start node-2 as it has game of life)

=> New view => Scripted => New item => gol-scripted-pipeline => pipeline => OK

  ![Alt text](shots/129.PNG)

* Pipeline can be written directly or can be chosen from source code management

=> Pipeline

  ![Alt text](shots/130.PNG)
  ![Alt text](shots/131.PNG)

* Open pipeline syntax

=> Pipeline syntax

  ![Alt text](shots/132.PNG)

=> Generate the syntax selecting the node allocation and copy into the script

  ![Alt text](shots/133.PNG)
  ![Alt text](shots/134.PNG)

* Creating the structure 

=> Repeat the above step of pipeline syntax for every possible manual step and complete the pipeline(Script)

  ![Alt text](shots/135.PNG)

* Sample pipeline
```
node('JDK_8') {
    stage('git') {
        git branch: 'master', url: 'https://github.com/Harika-SVL/game-of-life.git'
    }
    stage('build') {
        sh 'mvn package'
    }
    stage('reporting') {
        archiveArtifacts artifacts: '**/gameoflife.war', followSymlinks: false
        junit '**/surefire-reports/TEST-*.xml'
    }
}
```
### Create a Declartive Pipeline

* This has different structure in pipeline not for creating the project

* Create a spring-petclinic project (Start node-1 as it has spring-petclinic)

=> New view => Scripted => New item => spc-declarative-pipeline => pipeline => OK

  ![Alt text](shots/136.PNG)
  ![Alt text](shots/137.PNG)

* We have written
```
pipeline {
    agent { label 'JDK-17' } 
     stages() {
         stage('git') {
             steps {
                 git branch: 'main', url: 'https://github.com/Harika-SVL/spring-petclinic.git'
             }
         }
         stage('build') {
             steps {
                 sh 'mvn package'
             }
         }
     }   
    
}
```
### Scripted Pipelines

* Generally we create a file called as `Jenkinsfile`
* Basic structure: 
    [Refer Here : https://www.jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline]

  ![Alt text](shots/138.PNG)

* For all the steps 
    [Refer Here : https://www.jenkins.io/doc/pipeline/steps/]
* In scripted and declarative pipelines when we install plugins we get extra steps.

### Declarative Pipelines

* Here we create a file called as `Jenkinsfile`
* Basic structure: official docs 
    [Refer Here : https://www.jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline]

  ![Alt text](shots/139.PNG)

### Let's create a declarative pipeline for Spring-Pet-Clinic by exploring most options 

* For the repository
    [Refer Here : https://github.com/Harika-SVL/spring-petclinic.git]

  ![Alt text](shots/140.PNG)

* Let's create a `develop` branch

  ![Alt text](shots/141.PNG)

* Basic skeleton for a pipeline
```
pipeline {
    agent { label 'JDK-17' }
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JDK_17'
    }
    stages {
        stage('vcs') {
            steps {

            }
        }
        stage('build and package') {
            steps {

            }
        }
        stage('reporting') {
            steps {

            }
        }
    }

}
```
* Now using pipeline steps reference, let's do the build
    [Refer Here : https://www.jenkins.io/doc/pipeline/steps/]
* git 
    [Refer Here : https://www.jenkins.io/doc/pipeline/steps/git/#git-git]
* and also other steps 
```
pipeline{
    agent{ label 'JDK-17'}
    options{
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JDK_17'
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/Harika-SVL/spring-petclinic.git',
                    branch: 'develop'
            }
        }
        stage('build and package') {
            steps {
                sh script: 'mvn package'
            }
        }
        stage('reporting') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-*.jar'
                junit testResults: '**/target/surefire-reports/TEST-*.xml'
            }
        }
    }
}
```
    [Refer Here : https://github.com/dummyrepos/spring-petclinic-1/commit/303bcbbf79ca50d4e982dbf0fe017cef5af85101] 
  
* Now let's push the code to repository

  ![Alt text](shots/142.PNG)

* Create a project and build now

=> Declarative view => configure => pipeline 

  ![Alt text](shots/143.PNG)
  ![Alt text](shots/144.PNG)

* Build result

=> Save => Build Now

 ![Alt text](shots/145.PNG) 

#### Note:

* Create a free account in mailtrap 
    [Refer Here : https://mailtrap.io/]
* Exercise: Create a declarative pipeline
    * for spring-petclinic
    * for game-of-life

### Let's create a declarative pipeline for Game-of-Life  

* For the repository
    [Refer Here : https://github.com/Harika-SVL/game-of-life.git]

  ![Alt text](shots/146.PNG)

* Basic skeleton for a pipeline
```
pipeline {
    agent { label 'JDK_8' }
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JAVA_8'
    }
    stages {
        stage('code') {
            steps {

            }
        }
        stage('package') {
            steps {

            }
        }
        stage('report') {
            steps {

            }
        }
    }

}
```
* Now using pipeline steps reference, let's do the build
    [Refer Here : https://www.jenkins.io/doc/pipeline/steps/]
* git 
    [Refer Here : https://www.jenkins.io/doc/pipeline/steps/git/#git-git]
* and also other steps 
```
pipeline {
    agent { label 'JDK_8'}
    options {
        retry(3)
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JAVA_8'
    }
    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/Harika-SVL/game-of-life.git',
                    branch: 'master'
            }
        }
        stage('package') {
            steps {
                sh script: 'mvn clean package'
            }
        }
        stage('report') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: '**/target/gameoflife-*.war'
            }
        }
    }
}
```
    [Refer Here : https://github.com/dummyrepos/game-of-life-july23/commit/fb5bc9db8f2c376f2585703f84958e3363665537] 
  
* Let's use `master` branch
* Now let's push the code to repository

  ![Alt text](shots/147.PNG)

* Create a project 'gameoflife-declarative'and build now

=> Declarative view => New Item => name : gameoflife-declarative => pipeline => OK

  ![Alt text](shots/148.PNG)

=> Pipeline => Pipeline script from SCM => Git => URL : `https://github.com/Harika-SVL/game-of-life.git` => branch : `master` => path : `Jenkinsfile` => save

  ![Alt text](shots/149.PNG)
  ![Alt text](shots/150.PNG)

* Build result

=> Build Now

  ![Alt text](shots/151.PNG)

### Email Notifications

* For configuration 

  ![Alt text](shots/152.PNG)
  
* On Jenkins configuration

  ![Alt text](shots/153.PNG)

* Enter the credentials from mailtrap

  ![Alt text](shots/154.PNG)

* Set a random email and check for the email transfer

  ![Alt text](shots/155.PNG)

* Check on the mailtrap to confirm and save the changes into jenkins

  ![Alt text](shots/156.PNG)
  ![Alt text](shots/157.PNG)

#### Activity:

* Sending mail from pipeline
    [Refer Here : https://www.jenkins.io/doc/pipeline/steps/]
* To check for the ``SUCCESS` or `FAILURE` of the project we see the post section

* Lets send an email when the
    * project failed : `Your project is defective`
    * project success : `Your project is effective`
* Into the pipeline
```
pipeline {
    agent { label 'JDK_8'}
    options {
        retry(3)
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JAVA_8'
    }
    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/Harika-SVL/game-of-life.git',
                    branch: 'master'
            }
        }
        stage('package') {
            steps {
                sh script: 'mvn clean package'
            }
        }
        stage('report') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: '**/target/gameoflife.war'
            }
        }
    }
    post {
        success {
            mail subject: 'Your project is effective',
                 body: 'Your project is effective',
                 to: 'all@qt.com'
        }
        failure {
            mail subject: 'Your project is defective',
                 body: 'Your project is defective',
                 to: 'all@qt.com'
        }
    }
}
```
    [Refer Here : ]https://github.com/dummyrepos/game-of-life-july23/commit/e6b7d116df7f1dec1a5b6335a563e74def983185

* Here we just add the pipeline to the script from replay option

![Alt text](shots/158.PNG)

* For message with dynamic information
    [Refer Here : https://github.com/dummyrepos/game-of-life-july23/commit/956aaed06f6e78b8902b566794fd5811bd833c7d]
* I want to send microsoft teams/slack notification how to configure

### Parameters from Jenkinsfile

* For docs
    [Refer Here : https://www.jenkins.io/doc/book/pipeline/syntax/#parameters]
* For the changeset
    [Refer Here : https://github.com/dummyrepos/game-of-life-july23/commit/c8c92f3826fa7a121835d89040a7a30f5aa503ef]

### User Administration in Jenkins

* Authentication
    * Jenkins own user database
    * LDAP
    * Unix User/Group database
    * Redirect to Servlet
* Authorization:
    * Matrix
    * Role Based
* For screenshots refer to class room video

### Maven – Remote Repo

* Maven has 3 repositories
    * local repo (~/.m2)
    * Central repo: This is public maven repository
    * Remote Repo: This exists in organization controlled environment



* Workflows:
    * After every night build push the artifacts to remote repo
    * when resolving dependencies use remote repository

### Artifact Repository

* There are two popular options for java
    * jfrog/artifactory
    * Nexus
* Azure DevOps has Azure Artifacts
* In this series we will be using jfrog/artifactory for its multi language repository support.
* For 14 day free trail
    [Refer Here : https://jfrog.com/start-free/]



* For configuring jenkins with artifactory 
    [Refer Here : https://directdevops.blog/2019/10/17/artifactory-configuration/]
