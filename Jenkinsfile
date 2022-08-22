pipeline {
    agent any
     tools {
        maven 'Maven'
        }
    stages {
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test" 
            }

        }
        stage("Build"){
            steps{
                sh "mvn package"
            }

        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://65.0.85.96:8081')], contextPath: '/app', war: '**/*.war'
            }

        }
        stage("Deploy on Prod"){
             input {
                message "Should we continue?"
                ok "Yes we Should"
            }

            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://65.0.85.96:8081')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
