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
                script {
                    try {
                        // Code that might fail
                        sh 'echo "Running build process..."'
                        error 'Simulated error!' // Forces an exception
                    } catch (Exception e) {
                        // Handle the error/exception
                        echo "Caught an error: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                    } finally {
                        // Always runs whether it passes or fails
                        echo "Cleaning up workspace..."
                    }
                }
                
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
