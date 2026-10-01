pipeline {

  agent any
  stages {
    stage('Continuous Download')
    {
      steps 
      {
        // Source code address of maven repository
        git branch: 'main', url: 'https://github.com/sysgeeks4u/Maven-Tomcat.git'
      }
    }

    stage('Continuous Build')
    {
      steps 
      {
        // Building executable application
        sh 'mvn package'
      }
    }

    stage('Continuous Delivery')
    {
      steps 
      {
        // To deliver application on a QA Server
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'test-admin', path: '', url: 'http://172.31.22.81:8080')], contextPath: 'testapp', war: '**/*.war'
      }
    }
    
    stage('Continuous Testing')
    {
      steps 
      {
        // Testing application by using testing.jar file
        git branch: 'main', url: 'https://github.com/sysgeeks4u/Functional-Testing.git'
        
        // To run jar file
        sh 'java -jar /var/lib/jenkins/workspace/Declarative-Pipeline/testing.jar'
      }
    }

    stage('Continuous Deploy')
    {
      steps 
      {
        // Application deploying on live servers
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'prodserver_admin', path: '', url: 'http://172.31.24.228:8080')], contextPath: 'prodapp', war: '**/*.war'
      }
    }
  }

}
