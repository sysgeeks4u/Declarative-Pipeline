pipeline {
    agent any

    stages {
        stage('Continuouss Download') {
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
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'Tomcat-TestServer', path: '', url: 'http://172.31.45.67:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }

        stage('Continuous Test') {
            steps {
               git branch: 'main', url: 'https://github.com/sysgeeks4u/Functional-Testing.git'
               sh 'java -jar /var/lib/jenkins/workspace/Declartive-Pipeline/testing.jar'

            }
        }

        stage('Continuous Deploy') {
            steps {
               deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'TomcatProd', path: '', url: 'http://172.31.34.77:8080')], contextPath: 'prodapp', war: '**/*.war'

            }
        }
        
    }
}
