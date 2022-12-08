# Jenkins Demo

This project contains Jenkinsfile, notes and commands related to jenkins

## Jenkins Installation using Docker
1. docker run -p8080:8080 -p50000:50000 -v jenkins_home:/var/jenkins_home -d jenkins/jenkins:lts 

* Expose port 8080 - By default jenkins runs on this port
* Expose port 50000 - Master/Slave Communication
* Run in detached mode - Run container in the background
* Bind named volume - For data persistence in Jenkins
* **Tip** - Use --max-concurrent-downloads=1 if you have bandwidth issues while downloading

2. Copy the administrator password. This will be required while setting up jenkins - c5cc8a7c05274e22a26bc1dbfac7688c

3. Install the recommended plugins

## Types of Jenkins Projects
1. **Freestyle** - simple, single tasks e.g. run tests
2. **Pipeline** - whole delivery cycle e.g. build, test, deploy for single branch
3. **Multibranch Pipeline** - Same like pipeline but with multiple branches

Username/Password = jenkins-admin/jenkins-admin

## Credential Scopes
* **System** - Only available on Jenkins server, not on Jenkins Jobs
* **Global** - Everywhere accessible
* **Project** - Specific to Multi-branch pipeline ONLY

## Pipeline Syntax
| Scripted | Declarative |
| -------- | ----------- |
| First Syntax | Recent Addition |
| Groovy Engine | |
| Advanced Scripting, high flexibility | easier to get started but less powerful |
| No pre-defined structure | Pre-defined structure (template) |

## Required fields of Jenkinsfile
- *pipeline* - Must be top-level
- *agent* - Where to execute
- *stages* - Where the "work" happens

## Automatic Pipeline Trigger
There are two ways to automate triggering the pipeline:
1. **Push Notification:** Version control notifies Jenkins on new commit
    * Install Jenkins plugin based on your Version Control System
    * Configure Repository Server Hostname
    * Add Access Token or Credentials
2. **Polling:** Jenkins polls on a regular basis

## 4 Main Build Tools
* **Backend** - Maven, Gradle
* **Frontend** - Npm, Yarn

## Post Build Actions in Jenkinsfile
Execute some logic AFTER all stages executed: 
- always
- success
- failure

## Conditions/ When in Jenkinsfile
The steps are executed if the condition mentioned in 'when' block is true

## Environment Variables
Checkout the environment variables provided by Jenkins out of Box:
URL:- <URL of jenkins>/env-vars.html

### Credentials in Jenkins 
1. Define credentials in Jenkins UI
2. "credentials (credentialId)" binds the credentials
3. For that you need "credentials Binding" Plugin
4. You can reference these credentials as environment variable

### User-defined environment variable in Jenkins
Define user-defined variables in enviroment block of the Jenkins file

## Build Tools
Only 3 Build tools available:
* gradle
* maven
* jdk

## Parameters/ Parameterized your Build
Types of Parameter:
* **string** - string(name, defaultValue, description)
* **choice** - choice(name, choices, description)
* **booleanParam** - booleanParama(name, defaultValue, description)
