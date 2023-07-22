### Install – Jenkins

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

### Continuous Integration and Continuous Delivery/Deployment

* To perform frequent integrations and deployments we need a tool which can help us doing the same stuff and integrate with multiple tools. These tools are generallyt called as `CI/CD Engines`
* Jenkins is popular Opensource CI/CD Engine
* When we install jenkins we will have a user created called as jenkins
    * From jenkins we can perform anything which jenkins user can perform
* What happens when we install jenkins

![Alt text](shots/10.PNG)

* How can we integrte jenkins with any other tools:
    * Command line: call the command line
    * Plugin + installation/configuration:
      * UI or Pipeline step
* Refer in the classroom video for
    * Compiler vs interpretor vs hybrid
    * PATH variable
    * Environment variable

#### Note:
  * Adding sudo permission to Linux user [Refer Here: https://www.baeldung.com/linux/sudo-privileges-user]
```
sudo visudo

jenkins (ALL:ALL) NOPASSWD:ALL
```
### Dependencies

* Whenever a software project is developed, they have lot of dependencies
* before building the code, dependencies have to be present locally
* To manage these dependencies, every programming language has some kind of package manager
  * dotnet: nuget is the package manager
    * packages.config/packages.json
  * java: maven can handle package management
  * python: pip is the package manager
  * nodejs: npm can handle package management
* Scope of Work

![Alt text](shots/11.PNG)

## Maven

* Maven is a tool which can be use to build, package, distribute, test and generate documentation for java and java based languages
* Maven follows convention over configuration
* The maven uses a file called as pom.xml
* pom (Project object model)
* Maven Installation:
```
# install java 17
sudo apt update
sudo apt install openjdk-17-jdk -y
```
* Lets try installing maven 3.9.3 [Refer Here: https://maven.apache.org/download.cgi]
```
cd /tmp
wget https://dlcdn.apache.org/maven/maven-3/3.9.3/binaries/apache-maven-3.9.3-bin.tar.gz
sudo mkdir /usr/share/maven
sudo tar -xvzf apache-maven-3.9.3-bin.tar.gz -C /usr/share/maven
# add /usr/share/maven/apache-maven-3.9.3/bin to the PATH variable
# add to ~/.bashrc or /etc/environment
mvn --version
```



* Maven goals [Refer Here : https://www.baeldung.com/maven-goals-phases]
* Validate: validates the pom and it's project
* Compile: converts the java code into byte code (.java to .class). It stores the class files in `target/classes`
* Test: it will run the unit tests written and generates test results in xml format in text format. folder will be `/target/surefire-reports/TEST-*.xml`
* Package: creates the packaging format (jar/war/ear). will be `<artifact-id>-<version>.<packaging-format>`
* Install: This copies the package and its definition into M2_HOME or `~/.m2/repository`
* Deploy: copying package and its definition to remote repository for other users in other systems to use what you have built
* Clean: clean removes target folder
* Lifecycle [Refer Here : https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Lifecycle_Reference]
* To execute any lifecycle goal `mvn <goal>`
* We have written a simple pom
```
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
* Maven packaging formats: [Refer Here : https://www.baeldung.com/maven-packaging-types#:~:text=Maven%20offers%20many%20default%20packaging%20types%20that%20include%20a%20jar,and%20performs%20a%20specific%20task.]
* Maven goals downloads dependencies and stores in
  * `M2_HOME` where ever this environment variable points to and if not found does in `<home-dir>/.m2`

  ### Exercise

* Try installing maven as mentioned above
* Create a simple jenkins project
* build steps:
```
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic && mvn package
```
### Terms

* Artifact => For generating artifacts we use build tools msbuild, maven/gradle
* unit test => junit, mstest/nunit, pytest, jasmine, mocha, most ci cd systems understand junit xml reports to generate test results
* code coverage => we do this from sonar qube
* Static Code Analysis => we do this from sonar qube
* artifact repository => we would use jfrog (azure artifacts)