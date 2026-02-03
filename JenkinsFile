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

    stage('Continuous Deploy') 
    {
        steps
        {
        deploy adapters: [tomcat9(credentialsId: 'admin', path: '', url: 'http://54.81.255.134:8080')], contextPath: 'testapp', war: '**/*.war'
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
        deploy adapters: [tomcat9(credentialsId: 'admin', path: '', url: 'http://54.81.255.134:8080')], contextPath: 'prodapp', war: '**/*.war'
        }
    }
    
    }
}
