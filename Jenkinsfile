Skip to content
Search or jump to…
Pull requests
Issues
Codespaces
Marketplace
Explore
 
@ngehjulio 
ansahmdevops30
/
maven-web-application
Public
Fork your own copy of ansahmdevops30/maven-web-application
Code
Issues
Pull requests
Actions
Projects
Wiki
Security
Insights
Settings
Beta Try the new code view
maven-web-application/Jenkinsfile
@ngehjulio
ngehjulio Create Jenkinsfile
Latest commit 7f8578b 15 minutes ago
 History
 2 contributors
@ngehjulio@mylandmarktech
68 lines (60 sloc)  1.59 KB
 

pipeline{
  agent any 
  tools {
    maven "maven3.9.1"
  }  
  stages {
    stage('1GetCode'){
      steps{
        sh "echo 'cloning the latest application version' "
        git branch: 'feature', credentialsId: 'gitHubCredentials', url: 'https://github.com/ansahmdevops30/maven-web-application'
      }
    }
    stage('3Test+Build'){
      steps{
        sh "echo 'running JUnit-test-cases' "
        sh "echo 'testing must pass to create artifacts' "
        sh "mvn clean package"
      }
    }
    stage('4CodeQuality'){
      steps{
        sh "echo 'Perfoming CodeQualityAnalysis' "
        sh "mvn sonar:sonar"
      }
    }
   stage('5uploadNexus'){
      steps{
        sh "mvn deploy"
      }
    }  
    stage('8deploy2prod'){
      steps{
        deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://3.95.15.227:8177/')], contextPath: null, war: 'target/*war'  
        
      }
    }
}
    post{
       always{
      emailext body: '''Hey guys
Please check build status.
Thanks
Landmark 
+15147791676''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'paypal-team@gmail.com'
    }
success{
      emailext body: '''Hey guys,
Good job build and deployment is successful.
Thanks
Landmark
+15147791676''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'paypal-team@gmail.com'
    } 
failure{
      emailext body: '''Hey guys
Build failed. Please resolve issues.
Thanks
Landmark 
+15147791676''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'paypal-team@gmail.com'
  }
    }   
    
  }
