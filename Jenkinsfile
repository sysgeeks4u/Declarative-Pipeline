pipeline {
    agent any

    stages {
        stage('Continuous Download') {
            steps {
                git branch: 'main', url: 'https://github.com/sysgeeks4u/Maven-Tomcat.git'
            }
        }
        
        stage('Continuous Build') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Continuous Delivery') {
            steps {
              deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'test-admin', path: '', url: 'http://172.31.22.81:8080')], contextPath: 'testapp', war: '**/*.war'  
            }
        }

        stage('Continuous Test') {
            steps {
               git branch: 'main', url: 'https://github.com/sysgeeks4u/Functional-Testing.git'
               sh 'java -jar /var/lib/jenkins/workspace/Declarative-Pipeline/testing.jar'
            }
        }

        stage('Continuous Deploy') {
            steps {
               deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'prodserver_admin', path: '', url: 'http://172.31.24.228:8080')], contextPath: 'prodapp', war: '**/*.war'

            }
        }
        
    }
}
