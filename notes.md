## CI/CD Workflows

* There are 3 major workflow’s in which most of the projects fit in :
  * Virtual/ Physical Machine Deployment
  * Infra Provisioning and Deployment
  * Containerized Deployment

* Application Deployment Options : Applications are deployed on
  * Virtual Machines/ Physical Machines :
    * OnPrem
    * Cloud
  * Containers :
    * Kubernetes (OnPrem/Cloud)
  * Cloud Native Applications :
    * PaaS (Azure App Service/ AWS Elastic BeanStalk)
    * Faas (Azure Functions/AWS lambda)

* Activities

![Alt text](shots/212.PNG)

* Deployment

![Alt text](shots/213.PNG)

* Order of Execution

![Alt text](shots/214.PNG)

### Install-JENKINS

* [Refer here : https://www.jenkins.io/doc/book/installing/linux/] for installing Jenkins on Linux
* Installing on Ubuntu-steps: 
    [Refer here : https://www.jenkins.io/doc/book/installing/linux/#debianubuntu]
```
sudo apt update 
sudo apt install openjdk-17-jdk -y
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
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
* Jenkins is popular _**Opensource CI/CD Engine**_
* Any CI/CD tool at it's core is a `CRON on steroids`

#### CRONJOB In Linux - CRONTAB (periodic tasks on steroids)
  [Refer Here : https://crontab.guru/]

![Alt text](shots/215.PNG)

* _**CRON**_ is a Linux-based utility used to schedule scripts or programs
* The _**CRONTAB**_ is a list of commands that you want to run on a regular schedule, and also the name of the command used to manage that list. 
* Crontab stands for _**CRON TABLE**_, because it uses the job scheduler cron to execute tasks

SYNTAX : `<Minute> <Hour> <Day_of_the_Month> <Month_of_the_Year> <Day_of_the_Week> [command]`

![Alt text](shots/12.PNG)
![Alt text](shots/13.PNG)

* Minute => value : between 0-59
* Hour => value : between 0-23
* Day_of_the_month => value : between 1-31 
  * For the months having fewer days will ignore remaining part
* Month_of_the_year => value : between 1-12 
  * You can also define this value with the first three alphabets of the month like jan, feb, mar, apr etc.
* Day_of_the_Week => value : between 0-7
  *  Where 0 and 7 for Sunday, 1 for Monday, 2 for Tuesday, and so on. 
  * You can also use the first three alphabets of days like sun, mon, tue, wed, etc.

#### CRONJOB In Windows - TASK SCHEDULER
      
  [Refer Here : https://linuxhint.com/set-up-cron-job-windows/]

* In Windows, it is mostly utilized to automate the update system and scheduled tasks that will run automatically without manual execution. 
* If you want to create a new task or cron job on Windows, perform the required operation with the help of the `TASK SCHEDULER`

#### What happens when we install jenkins..?

* When we install jenkins we will have a `default user` created, _**JENKINS**_
* From jenkins we can perform anything which jenkins user performs

![Alt text](shots/10.PNG)

* How can we integrate jenkins with any other tools :
    * COMMAND LINE : call the command line
    * PLUGIN (Just gives an UI option to add in order to be converted to low level linux commands) + installation/configuration
      * UI or PIPELINE step

#### PATH variable 'echo $PATH'

  * To find path in linux `whereis <needed-name>`

#### Environment Variable

  * Every process in the system have their own ID and CPU, here Environmental variable stays common for all the processes in a system
  * System environmental variable(available to all the users present in a system) `sudo vi /etc/environment`
  * User environmental variable (available only to the specific user) `home/bashrc`

#### NOTE:
      
  * Adding sudo permission to Linux user 
          [Refer Here: https://www.baeldung.com/linux/sudo-privileges-user]
```
sudo visudo
jenkins (ALL:ALL) NOPASSWD:ALL
```
#### COMPILER vs INTERPRITOR vs HYBRID based applications :

* COMPILER-based application :

   [Dubbing before running the application] 

![Alt text](shots/14.PNG)

* INTERPRETOR-based application :

  [Translation during running of the application]

![Alt text](shots/15.PNG)

* HYBRID-based (both compiler and interpretor) application :

  [Before running the application the compilation is done to Intermediate Language and then through the Interpretor converts into server understandable]

![Alt text](shots/16.PNG)

![Alt text](shots/17.PNG)

### DEPENDENCIES

* Whenever a software project is developed, they have lot of dependencies
* Before building the code, dependencies have to be present locally
* To manage these dependencies, every programming language has some kind of _**package manager**_

[NOTE : `Package Management` is downloading the packages, building the packages and distributing the packages]

  * dotnet: `nuget` is the package manager
     * File to store the dependencies `packages.config/packages.json`
  * java: `maven` can handle package management
  * python: `pip` is the package manager
  * nodejs: `npm` can handle package management

### BUILD (every build) Workflow Structure

* Scope of Work :

![Alt text](shots/11.PNG)

### MAVEN

* Maven is a tool which can be used to build, package, distribute, test and generate documentation for java and java-based languages (groovy,scala)
* It follows convention (SNAPSHOT & RELEASE) over configuration
* It uses a file called as _**pom.xml**_ ( POM - Project Object Model )
* `Apache Log4j` Security Vulnerabilities

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

* Let's try installing MAVEN 3.9.6 

    [Refer Here: https://maven.apache.org/download.cgi]
```
cd /tmp/
wget https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
sudo mkdir /usr/share/maven
sudo tar -xvzf apache-maven-3.9.6-bin.tar.gz -C /usr/share/maven
# add `/usr/share/maven/apache-maven-3.9.6/bin` to the PATH variable
# add to `~/.bashrc` or `/etc/environment`
cd ~
sudo vi /etc/environment
# exit and relogin
mvn --version
```
![Alt text](shots/19.PNG)
![Alt text](shots/20.PNG)
![Alt text](shots/21-0.PNG)
![Alt text](shots/21.PNG)
![Alt text](shots/22.PNG)
![Alt text](shots/23.PNG)

#### MAVEN GOALS and LIFECYCLE :

  [Refer Here : https://www.baeldung.com/maven-goals-phases]

* VALIDATE : validates the _**pom**_ and it's project
* COMPILE : converts the _**java code**_ into _**byte code**_ (.java to .class). It stores the _**class files**_ in `target/classes`
* TEST : will run the _**unit tests**_ written and generates test results in _**xml format**_ of _**text format**_. Folder will be `/target/surefire-reports/TEST-*.xml`

![Alt text](shots/42.PNG)

* PACKAGE : creates the _**packaging format (jar/war/ear)**_ and will be `<artifact-id>-<version>.<packaging-format>`
* INSTALL : _**copies the package**_ and it's definition into `M2_HOME` or `~/.m2/repository`
* DEPLOY : copying package and it's definition to _**remote repository**_ for other users in other systems to use what you have built (This command is equivalent to `git push` command)
* CLEAN : _**removes**_ target folder

=> Here, when we execute a goal, all the pevious goals also get's executed

#### LIFECYCLE 
 
  [Refer Here : https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Lifecycle_Reference]
* To execute any lifecycle goal `mvn <goal>`
* Simple _**POM**_ file
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
* Maven _**PACKAGING FORMATS**_ : 

    [Refer Here : https://www.baeldung.com ]
* Maven goals downloads _**dependencies**_ and stores in
  * `M2_HOME` where ever this environment variable points to and if not found does in `<home-dir>/.m2`

  ### Exercise

* Try installing maven and create a simple jenkins project with following build steps :
```
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic/ 
mvn package
```
### MANUAL STEPS :

#### Installing JAVA-17
```
sudo apt update
sudo apt install openjdk-17-jdk -y
java --version
```
#### Installing MAVEN
```
cd /tmp/
wget https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
sudo mkdir /usr/share/maven
sudo tar -xvzf apache-maven-3.9.6-bin.tar.gz -C /usr/share/maven
cd ~
sudo vi /etc/environment
  # add '/usr/share/maven/apache-maven-3.9.6/bin'
exit
  # relogin into the machine
mvn -version
```
#### Building SPRING-PETCLINIC
```
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic/
mvn package 
```
### TERMS

* _**ARTIFACT**_ 

=> For generating artifacts we _**use build tools**_ like ms-build, maven/gradle

=> These are referenced in a _**pipeline stage**_ for automated deployment to the target environment

* _**UNIT TEST**_ 

=> java-junit, microsoft-mstest/nunit, python-pytest, nodejs-jasmine, nodejs-mocha, most CI/CD systems understand _**junit xml reports**_ to generate test results
            
=> incorporating unit testing into the DevOps process, which involves automating the entire software development life cycle to enable faster delivery of software while _**maintaining its quality**_

* _**CODE COVERAGE**_ 

=> we do this from `Sonar Qube`

=> helps you determine the proportion of your project's code that is actually being tested by tests such as _**unit tests**_. To increase your confidence of the code changes, and guard effectively against bugs, your tests should exercise - or cover - a large proportion of your code

[ _**Code Coverage**_ `=` _**Branch Coverage**_ (testing method, which aims to ensure that each one of the possible branch from each decision point is executed at least once and thereby ensuring that all reachable code is executed) `+` _**Line Coverage**_ (how many of lines of source code have been tested) ]

* _**STATIC CODE ANALYSIS**_ 

=> we do this from `Sonar Qube`, figuring `best code analysis`

=> method of computer program debugging that is done by examining the code without executing the program. The process provides an understanding of the _**code structure**_ and can help ensure that the code adheres to industry standards

* _**ARTIFACT REPOSITORY**_ 

=> we would use `jfrog (azure artifacts)`

=> Artifacts are _**large binary packages**_ that are created throughout the development and release process. An _**artifact repository**_ is a software application designed to manage these artifacts

### Building Maven projects using Jenkins  

#### JENKINS CONFIGURATION

* Install jenkins (jdk-17)
* Install and configure maven in Jenkins (Master Node)

    * Start a VM

      ![Alt text](shots/24.PNG)

    * Install Java-17

      ![Alt text](shots/25.PNG)

    * Install jenkins and configure as `jenkins user`

      ![Alt text](shots/26.PNG)

    * Add `jenkins`user to sudoers `sudo visudo`  WORKSPACE : `/var/lib/jenkins`

      ![Alt text](shots/27.PNG)
      ![Alt text](shots/28.PNG)

    * Install Maven as a `root-jenkins user`

      ![Alt text](shots/29-0.PNG)
      ![Alt text](shots/29.PNG)
    
* Let's build spring-petclinic 

    [Refer Here : https://github.com/spring-projects/spring-petclinic]

    * software requirements
      * jdk-17
      * maven

* Create a free style project to `build spring-petclinic`

=> New item => Freestyle project (name= spc-daybuild) => ok

![Alt text](shots/30.PNG)

* Free-style project sections

=> Description : This is to build spring-petclinic project 

1. _**GENERAL**_ : This represents the project information
      
    ![Alt text](shots/31.PNG)

2. _**SOURCE CODE MANAGEMENT**_ : This represent the code to be used for _**CI/CD pipelines**_

    ![Alt text](shots/32.PNG)

3. _**BUILD TRIGGERS**_ : represents when to build

  * `BUILD PERIODICALLY(CRON)` : If the project has to be _**built based on schedule**_, write cron expression into this 
  
    [Refer Here : https://crontab.guru/]

  * `POLL SCM` : represents jenkins _**polling scm**_ (asking git) and the cron expression represents how frequently it should ask. It is triggered only when there are changes in the code.

    ![Alt text](shots/33.PNG)

4. _**BUILD ENVIRONMENT**_ : represents the environmental configuration

   ![Alt text](shots/34.PNG)

5. _**BUILD STEPS**_ : actual activities that are performed during execution

   ![Alt text](shots/35.PNG)
   ![Alt text](shots/36.PNG)

6. _**POST BUILD ACTIONS**_ : actions to be performed after completion of build

   ![Alt text](shots/37.PNG)
   ![Alt text](shots/38.PNG)

* Now we can wait for the trigger to call the job or trigger build manually

 ![Alt text](shots/39.PNG)
 ![Alt text](shots/40.PNG)

* In Jenkins we can have multiple versions of java, maven, etc and we can handle these by configuring jenkins
* To fix the maven 3.6.3, issue we have to install 3.9.6 and use full path for package
```
cd /tmp/
wget https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
sudo mkdir /usr/share/maven
sudo tar -xvzf apache-maven-3.9.6-bin.tar.gz -C /usr/share/maven
cd spring-petclinic/
/usr/share/maven/apache-maven-3.9.6/bin/mvn package
```
* Go back and re-configure the maven version after finding the exact location fo maven `mvn`- `/usr/share/maven/apache-maven-3.9.6/bin`

![Alt text](shots/43.PNG)
![Alt text](shots/44.PNG)
![Alt text](shots/45.PNG)

* Test results

  ![Alt text](shots/46.PNG)
  ![Alt text](shots/41.PNG)
  ![Alt text](shots/42.PNG)

  ### TERMS :

* _**JENKINS_HOME**_ : Jenkins home is a folder where jenkins stores all of it's configuration. In the above case the workspace is `/var/lib/jenkins`. If you want to change the workspace deal with `JENKINS_HOME`

![Alt text](shots/28.PNG)

* Backup for Jenkins is backup of _**Workspace (/var/lib/jenkins)**_

* _**PROJECT**_ : This contains the activity that needs to be performed on triggers
    * This project is stored as _**xml file**_ in workspace
    * Types of projects :
      * FREESTYLE project: This is UI based configuration
      * PIPELINE: This is instructions expressed in some code format _**(pipeline as a code)**_

* _**BUILD**_ : This represents the execution of project. Every build for a project has a running number called as `Build_id`

* _**NODE**_ : This represents the machine on which build can be executed. Each Node can be configured to handle multiple builds by executors(no.of parallel working projects)

### Managing Different Versions of the tools using jenkins

* Connect to the jenkins installed VM 

=> Manage jenkins => Tools => Maven installations

  ![Alt text](shots/47.PNG)
  ![Alt text](shots/48.PNG)

* Connect to the machine through command line
```
sudo -i
su jenkins
cd /usr/share/maven (maven 3.6.3)
ls
cd /usr/share/maven/apache-maven-3.9.6   (maven 3.9.6)
```
  ![Alt text](shots/(a).PNG)
  ![Alt text](shots/(b).PNG)
  ![Alt text](shots/49.PNG)

* Now let's configure the spring-petclinic to use `top-level maven targets`

  ![Alt text](shots/50.PNG)

* Now build the project manually (`Build Now`)

  ![Alt text](shots/51.PNG)

### DISTRIBUTED BUILDS

* `Setup`:
  1. Fork Spring-petclinic   
      => spring-petclinic github => fork => owner,repo name => copy main branch only => create fork
      
      [Refer Here : https://github.com/Harika-SVL/Spring-petclinic]

    * requirements to build
        * java jdk-17
        * maven-3.9

  2. Fork Game-of-life 
      => game of life github => fork => owner,repo name => copy main branch only => create fork

      [Refer Here : https://github.com/Harika-SVL/Game-of-life]
    
    * requirements to build
        * java-8
        * maven

  3. Fork NopCommerce
      => nopcommerce github => fork => owner,repo name => copy main branch only => create fork

      [Refer Here : https://github.com/Harika-SVL/Nop-Commerce]
     
    * requirements to build
        * dotnet-7

  4. Fork Shopizer
      => shopizer github => fork => owner,repo name => copy main branch only => create fork

      [Refer Here : https://github.com/Harika-SVL/Shopizer]
     
  5. Fork BroadleafCommerce
      => broadleaf github => fork => owner,repo name => copy main branch only => create fork

      [Refer Here : https://github.com/Harika-SVL/Broadleaf-DemoSite]
    

* To handle different builds with different software needs, we tend to use different servers.
* Jenkins has distributed builds where we can distribute the builds on different nodes by matching labels
* While creating a project we can set labels and expect them to be executed on the node-matching labels

  ![Alt text](shots/53.PNG)

### How to add MULTIPLE NODES to jenkins

* Let's create 2 ubuntu VM's and let's make one VM as `Jenkins master` and the other as `node 1`

### Jenkins master => Java-17 and JENKINS

* On it install java-17,jenkins and configure jenkins and add the `user` to `sudoers`
```
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```
#### NOTE
=> To install jenkins we use the following script 
```
ls
sudo vi installjenkins.sh
```
### _**installjenkins.sh**_
```
#!/bin/bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
```
```
chmod +x installjenkins.sh
./installjenkins.sh
```
  ![Alt text](shots/54-0.PNG)

* Adding jenkins user to sudoers
```
sudo visudo
jenkins ALL=(ALL:ALL) NOPASSWD:ALL
```
* To check the sudoers
```
sudo -i
su jenkins
cd ~
sudo apt update
```
* Availing jenkins

  ![Alt text](shots/54.PNG)

### Node 1 => JDK-17 and MAVEN-3.9.6

* On this node (we use existing credentials) we will 
* Install java-17 
```
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```
* Install MAVEN-3.9.6
```
cd /tmp/
wget https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
sudo mkdir /usr/share/maven
sudo tar -xvzf apache-maven-3.9.6-bin.tar.gz -C /usr/share/maven
  # add `/usr/share/maven/apache-maven-3.9.6/bin` to the PATH variable in `/etc/environment`
cd ~
sudo vi /etc/environment
  # exit and relogin
mvn --version
```
  ![Alt text](shots/55.PNG)

[ Note => Jenkins credentials

  Username : JenkinsUser

  Password : JenkinsUser

  Name : JenkinsUser

  Mail : dummy@dummymail.com ]

* Now let's configure the _**Jenkins master**_ node with label `JDK-17`
* On Jenkins UI, navigate to 

=> Manage Jenkins => Nodes 

  ![Alt text](shots/56.PNG)

=> New node => name: node-1 , select Permanent agent => create

  ![Alt text](shots/57.PNG)

* Configuring the node-1 information

  ![Alt text](shots/58.PNG)
  ![Alt text](shots/59.PNG)

=> Host : private_ip (as both nodes in same network) => Credentials =>ADD : select Jenkins => select Kind and ID

  ![Alt text](shots/60.PNG)

=> add Description, Username => select Enter directly => add ssh-private key (cat id_rsa) => Add

  ![Alt text](shots/61.PNG)

=> Add Host, Credentials, Host key => Save

  ![Alt text](shots/62.PNG)

* node-1 gets connected

  ![Alt text](shots/63.PNG)

#### Let's setup Spring-PetClinic to execute on node-1

* Configure spc-day build same as last session with one restriction in General section

* Start a new project _**spc-Day-build**_

  ![Alt text](shots/64.PNG)

=> Select Source Code Management => Git : select new forked URL, BRANCH: main

  ![Alt text](shots/65.PNG)

=> Select Build Triggers => Poll SCM : * * * * *

  ![Alt text](shots/66.PNG)

=> select Build Steps => Invoke top-level maven targets => Goals : package => Save

  ![Alt text](shots/67.PNG)

=> go to Configure again => select When to run => add Label => Save

  ![Alt text](shots/68.PNG)

* Now build and verify the console output

  ![Alt text](shots/69.PNG)
  ![Alt text](shots/70.PNG)
  ![Alt text](shots/71.PNG)

* Now let's archive the artifacts `**/target/spring-petclinic-*.jar` add processing the test results `**/surefire-reports/TEST-*.xml`

  ![Alt text](shots/87.PNG)

* As a result of this project's build, I get `spring-petclinic-3.2.0-SNAPSHOT.jar` as below, which is called as `ARTIFACT`. Let's configure jenkins to Archive the Artifacts

  ![Alt text](shots/88.PNG)

### Node 2 => JDK-8 and MAVEN

* On the jenkins-master, we would require jdk-17 and for the project, `game-of-life`, we would require _**jdk-8**_
* On the node 2, let's create a `new user` called as _**devops**_ and add to `sudoers with NOPASSWD`
```
sudo adduser devops
  # password : devops
sudo visudo
  # devops  ALL=(ALL:ALL) NOPASSWD:ALL
```
* Now _**enable**_ password based authentication
```
sudo vi /etc/ssh/sshd_config
  # Change password Authentication to yes
sudo systemctl restart sshd
```
* Restart as _**devops**_ user
```
exit
ssh devops@<public_ip>
password : devops
```
* Install JDK-8, JDK-17 and MAVEN
```
sudo apt update
sudo apt install openjdk-8-jdk openjdk-17-jdk -y
java -version
cd /usr/lib/jvm
ls
cd ~
sudo apt install maven -y  
mvn -version
```
* Now execute java -version

  ![Alt text](shots/72.PNG)

* Let's configure JDK-17, JDK-8, Maven paths in tools section of jenkins `Jenkins master`
  ![Alt text](shots/73.PNG)
  ![Alt text](shots/159.PNG)

=> Also add `MAVEN_3.9` in the existing `spc-Day-build` project

* Now add Git - repository 'https://github.com/Harika-SVL/game-of-life.git' and `node 2` to jenkins

  ![Alt text](shots/74.PNG)

=> Configuring credentials `ADD`

  ![Alt text](shots/75.PNG)
  ![Alt text](shots/76.PNG)
  ![Alt text](shots/77.PNG)

* Now let's try building _**game-of-life**_ - Add JDK, MAVEN, Git and Save

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

* As a result of this project's build, we get _**gameoflife.war**_ which is called as `ARTIFACT`. Let's configure jenkins to `Archive the Artifacts`

  ![Alt text](shots/85.PNG)

=> Build Now

  ![Alt text](shots/86.PNG)

* _**NOTE**_ : We have implemented the same for `spring-petclinic`

  ![Alt text](shots/87.PNG)
  ![Alt text](shots/88.PNG)

* _**NOTE**_ : The health of the builds is represented as `Weather` in jenkins
    1. Cloudy - builds are failing
    2. Sunny - the builds are successful

  ![Alt text](shots/89.PNG)

### Node-3: Executing dotnet(.net) project on jenkins

* For agent we require JDK-17
* Create an ec2 instance (node 3)  with size 20 GB
* install dotnet-7 sdk for running Nop-Commerce
* Installation instructions :

  [Refer Here : https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-2204]
```
sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-7.0
dotnet --version
dotnet --help
```
  ![Alt text](shots/90.PNG)

* Configuring node 3 on Dashboard

  ![Alt text](shots/91.PNG)
  ![Alt text](shots/92.PNG)

=> Install JDK-17 on the node

  ![Alt text](shots/93.PNG)
  ![Alt text](shots/94.PNG)

* To build the dotnet project we need to restore nuget packages
```
cd /tmp/
git clone https://github.com/Harika-SVL/Nop-Commerce.git
ls
cd Nop-Commerce/
git branch
  ## dotnet restore <path of project or sln>
dotnet restore src/Nop-Commerce.sln
  ## dotnet build  -c "Release" <path of project or sln> 
dotnet build -c Release src/Nop-Commerce.sln
  ## For day builds
  ## dotnet build  -c "Debug" <path of project or sln> 
```
* Try to Configure in jenkins
* Create a new project

=> New Item => name : Nop-Commerce => Free-Style Project => OK

=> General => Restrict , Label : DOTNET_7

=> Source Code Management => Git : URL 'https://github.com/Harika-SVL/Nop-Commerce.git', Branch : master

=> Build Trrigers => Poll SCM : Schedule '* * * * * '

=> Build Steps => Execute shell : dotnet restore src/Nop-Commerce.sln , dotnet build -c Release src/Nop-Commerce.sln

=> Save

  ![Alt text](shots/160.PNG)

### Upstream and Downstream projects

* If the Project A triggers the Project B then
    * Project B is downstream of Project A
    * Project A is upstream of Project B

  ![Alt text](shots/95.PNG)

* Create a new view Project A, Project B, Project C

  ![Alt text](shots/96.PNG)

=> New item => Project A => Free-style Project => OK

=> Description : This is Project A => Buils steps : Execute shell : echo "Project A", sleep 10s => Save

  ![Alt text](shots/97.PNG)

* To connect the projects with each other

=> Project C => Configure => Build Triggers : Build after other projects are build : Project B => Save

  ![Alt text](shots/98.PNG)

[ OR ]

=> Project A => Configure => Post-build Actions : Build other projects : Project B => Trigger only if build is stable => Save

  ![Alt text](shots/99.PNG)

* Repeat above steps for Project B and Project C 

  ![Alt text](shots/100.PNG)
  ![Alt text](shots/101.PNG)
  ![Alt text](shots/102.PNG)
  
* Now build Project A and all the three projects get executed as they are connected and with a gap of 10sec each

  ![Alt text](shots/103.PNG)

### Parameterized Builds

* While building the Jobs, sometimes we would like users to pass some information. This is called as _**Parameters**_
* Create a New view with `list view` option

  ![Alt text](shots/104.PNG)
  

* Select the Jobs- _**game-of-life**_, _**Nop-Commerce**_, _**spc-Day-build**_

  ![Alt text](shots/105.PNG)
  ![Alt text](shots/106.PNG)

* Now let's enable parameters for some jenkins(game-of-life) project/job

  ![Alt text](shots/107.PNG)
  ![Alt text](shots/108.PNG)

* Create some parameters and use it in the `Build steps`

  ![Alt text](shots/109.PNG)
  ![Alt text](shots/110.PNG)

* Save and build the Goal

  ![Alt text](shots/111.PNG)
  ![Alt text](shots/112.PNG)
  ![Alt text](shots/113.PNG)
  ![Alt text](shots/114.PNG)

### Jenkins Environmental variables

* Jenkins injects environmental variables into every job, in addition to environmental variables present on the node
* To view environmental variables, select any project and navigate to Build steps => Execute shell

  ![Alt text](shots/115.PNG)
  ![Alt text](shots/115-1.PNG)
  ![Alt text](shots/116.PNG)

* Doc's on environmental variables
  
  [Refer Here : https://www.jenkins.io/doc/book/pipeline/jenkinsfile/#using-environment-variables]

* Sample using environmental variables (game-of-life on node 2 to print environmental variables)

=> Create New Project 'Environmentalvariablesdemo' in 'Experimental' view => General : JDK : JAVA_8, Restrict : JDK_8 => Build steps : Execute shell : printenv => Save => Build Now

* Result - Console Output

  ![Alt text](shots/117.PNG)

* Sample using Environmetal variables (Environmentalvariablesdemo)

=> Create New Project 'Environmentalvariablesdemo' in 'Experimental' view => Build steps : Execute shell :  echo "Hello, this project URL is ${JOB_DISPLAY_URL} and the BUILD-ID is ${BUILD_ID}", echo "Hello, this project is running in FOLDER ${WORKSPACE} on NODE ${NODE_NAME}" => Save => Build Now

  ![Alt text](shots/118.PNG)

* Result - Console Output

  ![Alt text](shots/119.PNG)
  
### How to take backup of jenkins...? (backup of /var/lib/jenkins folder)

* One option for backup is 'Configuration Files'

=> Manage Jenkins => Plugins => Available plugins => search : backup => Periodic Backup Manager

  ![Alt text](shots/120.PNG)
  ![Alt text](shots/121.PNG)

* To restart jenkins (only if you are admin)

=> refresh the page => relogin 

[ OR ]

=> In the Url : `http://18.60.61.74:8080/restart`

* Configuring the frequency for backup

=> Manage Jenkins => Periodic Backup Manager => Configure

  ![Alt text](shots/122.PNG)

  ![Alt text](shots/123.PNG)

  ![Alt text](shots/124.PNG)

  ![Alt text](shots/125.PNG)

=> Save => Backup Now

  ![Alt text](shots/126.PNG)

  #### Which plugin should be installed to monitor jenkins...?

  [Refer Here : https://plugins.jenkins.io/monitoring/]

* Monitoring option

=> Dashboard => Manage Jenkins => Plugins => Available plugins => search : monitoring => select :  Monitoring => select : Install without restart => select : Restart jenkins when no jobs running

  ![Alt text](shots/128.PNG)

* Jenkins Plugins can be installed from :
    * Market place
    * Uploading the plugin
* Jenkins plugin has two extensions :
    * jpi (Jenkins plugin interface)
    * hpi (hudson plugin interface) (old)

### Pipeline as Code

* This is expressing CI/CD pipleine in terms of some _**code/expressions/statements**_
* This is part of version control i.e. each change done to the steps will have history
* Official docs 
  
  [Refer Here : https://www.jenkins.io/doc/book/pipeline/pipeline-as-code/]

* Azure DevOps
```
# Starter pipeline
# Start with a minimal pipeline that you can customize to build and deploy your code
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

* Jenkins has two flavours : 
    1. Scripted Pipeline
        * Developed where you can execute groovy language directly
    2. Declartive Pipeline
        * Jenkins has created a DSL (Domain Specific Language) which is mostly inspired from traditional jenkins

#### Creating a Scripted Pipeline

* Create a Game-of-life project (Start node 2 as it has game-of-life)

=> New view => name : Scripted => New item => name : gol-scripted-pipeline => Pipeline => OK

  ![Alt text](shots/129.PNG)

* Pipeline can be written directly or can be chosen from Source Code Management

=> Pipeline

  ![Alt text](shots/130.PNG)
  ![Alt text](shots/131.PNG)

* Open Pipeline Syntax

=> Pipeline Syntax

  ![Alt text](shots/132.PNG)

=> Generate the syntax selecting the `Node:allocation` and copy into the script

  ![Alt text](shots/133.PNG)
  ![Alt text](shots/134.PNG)

* _**Creating the structure**_ 

=> Repeat the above steps of pipeline syntax for every possible manual step and complete the pipeline(Script)

  ![Alt text](shots/135.PNG)

* _**Sample pipeline**_
```
node('JDK_8') {
    stage('git') {
        git branch: 'master', url: 'https://github.com/Harika-SVL/Game-of-life.git'
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

* This has _**different structure in pipeline**_ not for creating the project

* Create a spring-petclinic project (Start node-1 as it has spring-petclinic)

=> New view => name : Declarative => New item => spc-declarative-pipeline => Pipeline => OK

  ![Alt text](shots/136.PNG)
  ![Alt text](shots/137.PNG)

* We have written
```
pipeline {
    agent { label 'JDK-17' } 
     stages() {
         stage('git') {
             steps {
                 git branch: 'main', url: 'https://github.com/Harika-SVL/Spring-petclinic.git'
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
* In Scripted and Declarative pipelines when we install plugins we get extra steps.

### Declarative Pipelines

* Here we create a file called as `Jenkinsfile`
* Basic structure: official doc's 
    
    [Refer Here : https://www.jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline]

  ![Alt text](shots/139.PNG)

### Let's create a declarative pipeline for Spring-petclinic by exploring most options 

* For the repository
    
    [Refer Here : https://github.com/Harika-SVL/Spring-petclinic.git]

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
                git url: 'https://github.com/Harika-SVL/Spring-petclinic.git',
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

=> Declarative view => configure => Pipeline 

  ![Alt text](shots/143.PNG)

=> mention the script path as the filename given to store the code (Jenkinsfile, code, etc)

  ![Alt text](shots/144.PNG)

* Build result

=> Save => Build Now

  ![Alt text](shots/145.PNG)

#### Note:

* Create a free account in mailtrap 

    [Refer Here : https://mailtrap.io/]

### Let's create a declarative pipeline for Game-of-Life  

* For the repository
  
  [Refer Here : https://github.com/Harika-SVL/Game-of-life.git]

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
                git url: 'https://github.com/Harika-SVL/Game-of-life.git',
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
}
```
  [Refer Here : https://github.com/dummyrepos/game-of-life-july23/commit/fb5bc9db8f2c376f2585703f84958e3363665537] 
  
* Let's use `master` branch
* Now let's push the code to repository

  ![Alt text](shots/147.PNG)

* Create a project 'gol-declarative-pipeline' and Build Now

=> Declarative view => New Item => name : gol-declarative-pipeline => Pipeline => OK

  ![Alt text](shots/148.PNG)

=> Pipeline => Pipeline script from SCM => Git => URL : https://github.com/Harika-SVL/Game-of-life.git => Branch : master => Path : Jenkinsfile => Save

  ![Alt text](shots/149.PNG)
  ![Alt text](shots/150.PNG)

* Build and Result

=> Build Now

  ![Alt text](shots/151.PNG)

### Email Notifications

* For configuration - on mailtrap account

  ![Alt text](shots/152.PNG)
  
* On Jenkins configuration

=> Manage Jenkins => System

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

* To check for the `SUCCESS` or `FAILURE` of the project we use the _**Post**_ section

* Let's send an email, when the project,
    1. Fail : `Your project is defective`
    2. Success : `Your project is effective`

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
                git url: 'https://github.com/Harika-SVL/Game-of-life.git',
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
  [Refer Here : https://github.com/dummyrepos/game-of-life-july23/commit/e6b7d116df7f1dec1a5b6335a563e74def983185]

* Here we just add the pipeline to the script from `Replay` option

  ![Alt text](shots/158.PNG)

  ![Alt text](shots/161.PNG)

* For message with `Dynamic information`
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
                git url: 'https://github.com/Harika-SVL/Game-of-life.git',
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
            mail subject: '${JOB_NAME}: has completed with success',
                 body: 'Your project is effective \n Build Url ${BUILD_URL}',
                 to: 'all@qt.com'
        }
        failure {
            mail subject: '${JOB_NAME}: has not been completed and failed',
                 body: 'Your project is defective \n Build Url ${BUILD_URL}',
                 to: 'all@qt.com'
        }
    }
}
```
  ![Alt text](shots/162.PNG)
  ![Alt text](shots/163.PNG)
  

=> Use double quotes("") instead of single quotes('') (Let's `Replay to change`)
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
                git url: 'https://github.com/Harika-SVL/Game-of-life.git',
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
            mail subject: "${JOB_NAME}: has completed with success",
                 body: "Your project is effective \n Build Url ${BUILD_URL}",
                 to: 'all@qt.com'
        }
        failure {
            mail subject: "${JOB_NAME}: has completed with failed",
                 body: "Your project is defective \n Build Url ${BUILD_URL}",
                 to: 'all@qt.com'
        }
    }
}
```
   ![Alt text](shots/164.PNG)
   ![Alt text](shots/165.PNG)
  
  [Refer Here : https://github.com/dummyrepos/game-of-life-july23/commit/956aaed06f6e78b8902b566794fd5811bd833c7d]

* I want to send message on `Microsoft Teams/Slack` notification how to configure [ Google search ]

### Parameters from Jenkinsfile

* For doc's
    
    [Refer Here : https://www.jenkins.io/doc/book/pipeline/syntax/#parameters]
```
pipeline {
    agent { label 'JDK_8' }
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
    parameters {
        choice(name: 'GOAL', choices: ['package', 'clean package', 'install', 'clean install'], description: 'This is maven goal')
    }
    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/dummyrepos/game-of-life-july23.git',
                    branch: 'master'
            }
        }
        stage('package') {
            steps {
                sh script: 'mvn clean package'
                sh script: "mvn ${params.GOAL}"
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
            mail subject: "${JOB_NAME}: has completed with success",
                 body: "your project is effective \n Build Url ${BUILD_URL}",
                 to: 'all@qt.com'
        }
        failure {
            mail subject: "${JOB_NAME}:: has completed with failed",
                 body: "your project is defective \n Build Url ${BUILD_URL}",
                 to: 'all@qt.com'
        }
    }
}
```
   ![Alt text](shots/166.PNG)
   ![Alt text](shots/166-1.PNG)
    
  [Refer Here : https://github.com/dummyrepos/game-of-life-july23/commit/c8c92f3826fa7a121835d89040a7a30f5aa503ef]

### User Administration in Jenkins (user specific permissions)

* Authentication (where for given permission)
    * Jenkins own user database
    * LDAP
    * Unix User/Group database
    * Redirect to Servlet
* Authorization (where it is allowed/not allowed)
    * Matrix
    * Role-Based

  ![Alt text](shots/167.PNG)
  ![Alt text](shots/168.PNG)

* Creating users and adding permissions as above

  ![Alt text](shots/169.PNG)
  ![Alt text](shots/170.PNG)

  * Add `Role-based Strategy` plugin 

=> Dashboard => Manage jenkins => Plugins => search : Role-Based Strategy => Install with restart => Restart when no jobs running

  ![Alt text](shots/172.PNG)

* Add Role-based strategy

=> Dashboard => Manage jenkins => Security => select : Role-based strategy => Save

* Add a user to give permissions

=> Manage Jenkins => Manage and Assign Roles => Manage Roles => add `developer` user, `qa` user => Add

  ![Alt text](shots/173.PNG)
  ![Alt text](shots/174.PNG)

* Assign the role to a user by creating one

  ![Alt text](shots/175.PNG)

* Restart the jenkins page `http://18.61.90.194:8080/restart` and Login as `dummy` user

  ![Alt text](shots/176.PNG)

### Maven – Remote Repo

* Maven has 3 repositories : 
    * Local Repo : (~/.m2)
    * Central Repo : This is public maven repository
    * Remote Repo : This exists in organization controlled environment

  ![Alt text](shots/177.PNG)

* Workflows:
    * After every night build, push the artifacts to remote repo
    * When resolving dependencies, use remote repository

### Artifact Repository

* There are two popular options for java : 
    * jfrog/artifactory
    * Nexus
* Azure DevOps has Azure Artifacts
* In this series we will be using jfrog/artifactory for it's multi language repository support
* For 14-day free trail
  
  [Refer Here : https://jfrog.com/start-free/]

* Create an account(14-day trail) and proceed

  ![Alt text](shots/178.PNG)

* Crete a new repo for maven

  ![Alt text](shots/179.PNG)

=> URL of repo : `https:///artifactory/api/maven/qt-libs-snapshot`

=> Setup maven client

  ![Alt text](shots/180.PNG)

=> Token generated : `cmVmdGtuOjAxOjE3MjM1NjQyNjc6T09kRTZkZFpNT2tkNDZrYlJMdlp1VjBDQnRU`

=> Go to .m2 folder ( C:\Users\Harika\.m2) => Create `settings.xml` 

  ![Alt text](shots/181.PNG)

=> Configuring settings.xml => Generate settings

  ![Alt text](shots/182.PNG)
  ![Alt text](shots/183.PNG)

=> Removing settings.xml

  ![Alt text](shots/184.PNG)

[ NOTE : Instead using local repo configuring like above we try to configure over jenkins as below ]

* For configuring jenkins with artifactory 
  
  [Refer Here : https://directdevops.blog/2019/10/17/artifactory-configuration/]

=> Manage Jenkins => Plugins => Available plugins => artifactory => select : Artifactory, Jfrog => Install without restart =>  Restart when no jobs running

  ![Alt text](shots/185.PNG)

=> Relogin => Dashboard => Manage Jenkins => System => JFrog plugin configuration => Add JFrog platform instance

  ![Alt text](shots/186.PNG)

=> Leave
=====================================================================================================================
* To integrate jenkins with JFrog
=> Dashboard => Manage Jenkins => Credentials => system => Global credentials => Add credentials
  ![Alt text](shots/187.PNG)
  ![Alt text](shots/188.PNG)
[ NOTE : To generate new token if required
       => Generate an Identity Token]
=> Dashboard => Manage Jenkins => System 
  ![Alt text](shots/189.PNG)
* For setting Artifactory
* Create a new user
  ![Alt text](shots/190.PNG)
  ![Alt text](shots/191.PNG)
  ![Alt text](shots/192.PNG)
=> Dashboard => Manage Jenkins => System => JFrog => Use the Credentials Plugin => Add JFrog Platform Instances   
  ![Alt text](shots/193.PNG)
  ![Alt text](shots/194.PNG)
* DELETING THE PLUGINS INSTALLED TILL NOW
======================================================================================================================

### Artifactory Jenkins Integration 

* Create an access token after Jfrog account creation

=> open jfrog.io [ URL : https://haarisvl95.jfrog.io/ ]=> Artifactory (on left) => Repositories => Create a Repository => select : maven => name : qt-app => Create

  ![Alt text](shots/195.PNG)

  URL : https://haarisvl95.jfrog.io/artifactory/api/maven/qt-app-libs-snapshot

=> I'll do it later

* Creating a new group

=> New Group (in right dropdown) => Groups => New Group

  ![Alt text](shots/196.PNG)

* Add users

  ![Alt text](shots/197.PNG)

* Generating Token

=> Access Token => Generate Token

  ![Alt text](shots/198.PNG)

  Token : eyJ2ZXIiOiIyIiwidHlwIjoiSldUIiwiYWxnIjoiUlMyNTYiLCJraWQiOiIwWE93Y0FkWDIybDJ6Z1l2T0FLd3hRVEtxX2l6NnVCSnJuZHlPaHFUNUs0In0.eyJzdWIiOiJqZmFjQDAxaDdteHRhYmRwejk4MDNmZWZobncwcWJ3L3VzZXJzL2Rldm9wcyIsInNjcCI6ImFwcGxpZWQtcGVybWlzc2lvbnMvYWRtaW4iLCJhdWQiOiIqQCoiLCJpc3MiOiJqZmZlQDAxaDdteHRhYmRwejk4MDNmZWZobncwcWJ3IiwiZXhwIjoxNjk0Njc4MTMxLCJpYXQiOjE2OTIwODYxMzEsImp0aSI6IjcyMmNiY2Q5LTJiNDMtNDAwOS04ZjFhLTE4OTA1NDEzMzBlYSJ9.uy0_MSd2sTgDlhBVWa19At83G0NyoAsx9tlAteRRjpagL0Cw085ECKdggcFOk7Nv3I7sELgxyrGFGkpEFn9Jdy30fAcW4PL1GpakEzQ2NSYlrla4zYoorHKi5JHwZb42vI4cY-qBh076GEqjA9ysDxDxwcgu4pxBmTAcnzYke27RWwqgjmIw-ebcuZqvsB3hfo4RL-QkqDqD13Rv4K-3rBXS5g5ASBiatq3oGz1znlCJjgv675A6-qEcnHxLUdTbH294SNRA37ycXWe2qso_uMNgjKnB4-tUxz5L3KCKZRrwIJrdSU3hiZTQFF_hs0o0YUkW4PtDAc_mqlj05iPnRg

* Install artifactory plugin in jenkins

=> Install plugin and restart

  ![Alt text](shots/199.PNG)

=> Manage Jenkins => Credentials => System => Global Credentials => Create credentials 

  ![Alt text](shots/200.PNG)
  ![Alt text](shots/201.PNG)

* Configuring system

=> Manage Jenkins => System => Jfrog

  ![Alt text](shots/202.PNG)
  ![Alt text](shots/203.PNG)
  ![Alt text](shots/204.PNG)

* Creating a maven project and using jfrog

=> New Item => name : spc-maven-jfrog => Maven Project => OK

=> Git : select URL : https://github.com/Harika-SVL/spring-petclinic.git => Branch : main

  ![Alt text](shots/205.PNG)

=> Build => Goals and options : package

  ![Alt text](shots/206.PNG)

=> Post-build Actions => Deploy artifacts to Artifactory => Refresh Repositories 

  ![Alt text](shots/208.PNG)

=> Build Now

  ![Alt text](shots/209.PNG)
  ![Alt text](shots/210.PNG)

* For official doc's of Jfrog artifactory pipeline

  [ Refer here : https://jfrog.com/help/r/jfrog-integrations-documentation/jenkins-artifactory-plug-in]
* For samples of Jfrog jenkins pipelines

  [ Refer Here : https://github.com/jfrog/project-examples/tree/master/jenkins-examples/pipeline-examples/declarative-examples]
* For specific Jenkinsfile

  [ Refer Here : https://github.com/jfrog/project-examples/blob/master/jenkins-examples/pipeline-examples/declarative-examples/maven-example/Jenkinsfile]
* The pipeline example
* Create a new project

=> Dashboard => New Item => name : spc_pipeline => Pipeline => OK

=> Pipeline => Script

  ![Alt text](shots/211.PNG)
```
pipeline {
    agent any
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
                git url: 'https://github.com/Harika-SVL/spring-petclinic.git',
                    branch: 'develop'
            }
        }
        stage('build and package') {
            steps {
                 rtMavenDeployer (
                    id: "SPC_DEPLOYER",
                    serverId: "JFROG_CLOUD",
                    releaseRepo: 'qt-app-libs-snapshot-local',
                    snapshotRepo: 'qt-app-libs-snapshot-local'
                )
                rtMavenRun (
                    tool: 'MAVEN_3.9', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "SPC_DEPLOYER"
                    //,
                    //buildName: "${JOB_NAME}",
                    //buildNumber: "${BUILD_ID}"
                )
                rtPublishBuildInfo (
                    serverId: "JFROG_CLOUD"
                )
            }
        }
        stage('reporting') {
            steps {
                junit testResults: '**/target/surefire-reports/TEST-*.xml'
            }
        }
    }

}
```
=> Save => Build Now



### Static Code Analysis

* For this, let's use Sonar Cloud
* For Configuration doc's

  [ refer Here : https://docs.sonarcloud.io/advanced-setup/ci-based-analysis/jenkins-extension-for-sonarcloud/#:~:text=Configure%20SonarCloud%3A,created%20as%20a%20]
* To create SonarQube Cloud account

  [ Refer Here : https://www.sonarsource.com/products/sonarcloud/signup/]
* Now let's create a SonarQube Static Code Analysis
* For configuring and installing SonarQube

  [ Refer Here : https://directdevops.blog/2019/01/05/sonarqube/]
* The pipeline
```
pipeline {
    agent any
    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JDK_17_UBUNTU'
        maven 'MAVEN_3.9'
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/dummyrepos/spring-petclinic-1.git',
                    branch: 'develop'
            }
        }
        stage('SonarQube analysis') {
            steps {

                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                withSonarQubeEnv('SONAR_CLOUD') {
                // requires SonarQube Scanner for Maven 3.2+
                    sh 'mvn clean package sonar:sonar -Dsonar.organization=khajaprojectsjuly23 -Dsonar.token=67d5cbb26a76f3a1c2c669a0d7be62e66722c488 -Dsonar.projectKey=springpetclinic'
                }
            }
        }


        stage('reporting') {
            steps {
                junit testResults: '**/target/surefire-reports/TEST-*.xml'
            }
        }
    }

}
```






[ NOTE: For different ecosystem 

  [ Refer Here : https://learn.microsoft.com/en-us/azure/devops/pipelines/ecosystems/ecosystems?view=azure-devops] ]

### Branching Strategy

* Git Flow: 
    
  [Refer Here : https://directdevops.blog/2019/01/04/best-branching-strategy-git-flow/]
* Also refer the following branching strategy
    * Gitlab
    * GitHub

### Pull-request

* Consider this original repository 

  [Refer Here : https://github.com/GitPracticeRepo/prdemojuly23]

### Workshop – Project

* Project 

  [Refer Here : https://github.com/nopSolutions/nopCommerce]
* We will create a pull request based workflow



* Release Branch (Night build)
  * Docker/Container based workflow (DevSecOps)
    * Security Scans
      * SCA
      * SAST
      * DAST
    * From terraform
      * Kubernetes cluster
      * Deploy application
  * VM based Workflow
    * From Terraform
      * VM
      * Database

[Refer Here : https://directdevops.blog/2023/03/11/devops-classroomnotes-11-mar-2023-2/] and [Refer Here : https://directdevops.blog/2023/03/11/devops-classroomnotes-11-mar-2023/] before tomorrow’s session

## CI/CD Pipeline Based on Jenkins – Workshop

### Virtual Machine or Cloud Based Deployment

* We will be building a CI/CD Pipeline of a .net platform based application

### Steps

  1. Jenkins Master and Node setup
      * Node:
         * os: ubuntu
         * software:
            * openjdk17 (jenkins)
            * .net 7 sdk
            * git
            * zip
  2. Build steps:
```
git clone https://github.com/CICDProjects/nopCommerceJuly23.git
dotnet restore src/NopCommerce.sln
dotnet build -c Release src/NopCommerce.sln
dotnet publish -c Release src/Presentation/Nop.Web/Nop.Web.csproj -o publish
mkdir publish/bin publish/logs
zip -r nopCommerce.zip publish
```
  1. Now create a Jenkins file, in such a way that when a commit happens on develop branch the build creates a nopCommmerce zip file.
  2. solution for the jenkins file
     
  [Refer here : https://github.com/CICDProjects/nopCommerceJuly23/commit/62fdd0c1e1493566a7f94b1daa1f6ad90c422fa2]

### Container Based Deployment

### Steps

  1. Jenkins Master and Node setup
          * Node:
                * os: ubuntu
                * software:
                      * Docker
                      * steps:
                          * curl -fsSL https://get.docker.com -o install-docker.sh
                          * sudo sh install-docker.sh
                          * sudo usermod -aG docker jenkins
                            [NOTE: jenkins represents the user on the node]
                          * restart jenkins server
  2. Build steps
```
git clone https://github.com/CICDProjects/nopCommerceJuly23.git
# replace latest with Git Commit id or build id
docker image build -t nopCommerce:latest .
#docker image tag nopCommmerce:latest shaikkhajaibrahim/nopCommerce:latest
#docker image push shaikkhajaibrahim/nopCommerce:latest
```
  * Write Jenkinsfile for the above steps

### Creating kubernetes cluster from terraform

* For the changes

    [Refer here : https://github.com/CICDProjects/nopCommerceJuly23/commit/4d26cd8e07507075946a99e49097e0f8407fe051]
* Workflow





* For the k8s manifest

    [Refer here : https://github.com/CICDProjects/nopCommerceJuly23/commit/62fdd0c1e1493566a7f94b1daa1f6ad90c422fa2]
* Softwares
    * Terraform
    * azure cli
    * kubectl
* Manual deployment steps
```
cd deploy
terraform init
terraform apply -auto-approve
az aks get-credentials --resource-group rg-national-cod --name cluster-star-goat
kubectl apply -f ../k8s/nop-deploy.yaml
```
* For changes in jenkins file

    [Refer here : https://github.com/CICDProjects/nopCommerceJuly23/commit/1e31820e3b86fecd18754543f8ef78f9027e237c]

### Git Alias

  [Refer here : https://www.atlassian.com/git/tutorials/git-alias]

### Git Hooks

  [Refer here : https://directdevops.blog/?s=hooks]




* Navigate to hooks section

  [Refer here : https://directdevops.blog/2023/03/11/devops-classroomnotes-11-mar-2023/]
* For popular hooks

  [Refer here : https://github.com/aitemr/awesome-git-hooks]
* Since for hosted git repo’s like GitHub, GitLab we have no access to hooks folder, they give us webhooks 




  [Refer here : https://www.blazemeter.com/blog/how-to-integrate-your-github-repository-to-your-jenkins-project]
* for github actions approach instead of webhookF

  [Refer here : https://mickeygousset.com/blog/trigger-jenkins-pipeline-with-github-actions/]

### Git stash

* For stash doc's

  [Refer here : https://www.atlassian.com/git/tutorials/saving-changes/git-stash]

