pipeline {
    agent any

    tools{
        maven 'mvn-3.8.6'  //This 'mvn-3.8.6' is the name we've  given to Maven installation in Jenkins
    }

    environment {
        NEW_VERSION='1.0.1'
        // These credentials are created in Jenkins UI. 'server-credentials' is the ID of the credentials
        SERVER_CREDENTIALS = credentials('server-credentials') 
    }

    parameters {
        // string(name: 'VERSION', defaultValue: '', description: 'Version to deploy to Production')
        choice(name: 'VERSION', choices: ['1.0', '2.0'], description: 'Version to deploy to Production')
        booleanParam(name: 'executeTests', defaultValue: true, 'Execute Tests?')
    }

    stages {
        stage("build"){
            steps{
                echo "Building demo project"
                echo "Building version: ${NEW_VERSION}"
                sh "mvn install" // tools section defined above has made the mvn command available here
            }
        }

        stage("unitTest"){
            when {
                expression {
                    BRANCH_NAME == 'dev' || BRANCH_NAME == 'feature'
                }
            }
            steps{
                echo "Testing demo project"
            }
        }
        stage("integrationTest"){
            when{
                expression{
                    params.executeTests == true
                }
            }
        }
        stage("deploy"){
            steps{
                echo "Deploying demo project"
                echo "Deploying with ${SERVER_CREDENTIALS}"
                sh "${SERVER_CREDENTIALS}"

                // Or you can use withCredentials wrapper
                withCredentials([
                    usernamePassword(credentials: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)
                ]){
                    sh "some script ${USER} ${PWD}"
                }
                
            }
        }
    }
    post {
        always {
            echo "This will always execute"
        }
        success {
            echo "This will execute only when pipeline stages executed successfully"
        }
        failure{
            echo "This will execute only when pipeline fails"
        }
    }
}
