pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '13.232.37.20', description: 'Remote Staging Server')
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            steps{
                  deploy adapters: [tomcat8(credentialsId: '801cd8f0-c34e-49d3-8f21-26d9faca7c84', path: '', url: 'http://localhost:8081/')], contextPath: null, war: '**/*.war'
                   
            }
        }
    }
}
