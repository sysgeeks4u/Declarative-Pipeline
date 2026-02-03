pipeline 
{
    agent any

    stages
    {
     stage('Continuous Download') 
    {
        steps
        {
        git branch: 'main', url: 'https://github.com/sysgeeks4u/Maven-Tomcat.git'
        }
    }

    stage('Continuous Build') 
    {
        steps
        {
        sh 'mvn package'
        }
    }

    stage('Continuous Delivery') 
    {
        steps
        {
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcattest', path: '', url: 'http://172.31.24.35:8080')], contextPath: 'testapp', war: '**/*.war'
        }
    }

    stage('Continuous Test') 
    {
        steps
        {
        git branch: 'main', url: 'https://github.com/sysgeeks4u/Functional-Testing.git'

        sh 'java -jar /var/lib/jenkins/workspace/Testing/testing.jar'
        }
    }

    stage('Continuous Delivery') 
    {
        steps
        {
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcatprod', path: '', url: 'http://172.31.68.42:8080')], contextPath: 'prodapp', war: '**/*.war'
        }
    }
    
    }
}
