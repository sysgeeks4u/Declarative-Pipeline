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

        sh 'java -jar /var/lib/jenkins/workspace/DEC-PIPELINE/testing.jar
        }
    }

    stage('Continuous Deploy') 
    {
        steps
        {
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcatprod', path: '', url: 'http://172.31.68.42:8080')], contextPath: 'prodapp', war: '**/*.war'
        }
    }
    
    }

    post
      {
            always
            {
            echo 'This always runs at the very end of the pipeline.'
            }
           success
           {
             echo 'The entire Pipeline was successful.'
           }
            failure
           {
             echo 'The entire Pipeline failed.'
             // Example: Send a notification email.
             mail bcc: '', body: 'CI CD & CD Project Process', cc: 'rnraju4u@gmail.com', from: '', replyTo: '', subject: 'CI_CD_FAILD', to: 'ram.ashokit@gmail.com'
           }
       }

}
