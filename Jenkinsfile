pipeline {
  agent any 
  tools {
     maven 'M2_HOME'
        }
stages {
     stage('Git Checkout') {
       steps {
         git 'https://github.com/devopscbabu/24-Apr-Insureme.git'
             }
        }
     stage('Build Package') {
       steps {
         sh 'mvn package'
       }
     }
     stage('Publish HTML Reports') {
       steps {
         publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/InsureProject/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
             }
         }
     stage('Create Docker image of App') {
       steps {
         sh 'docker build -t cbabu85/insure-me-app:1.0 .'
             }
         }
     stage('Docker Image Push') {
       steps {
         withCredentials([usernamePassword(credentialsId: 'docker-hub-2', passwordVariable: 'docker_password', usernameVariable: 'docker_login')]) {
         sh 'docker login -u ${docker_login} -p ${docker_password}'
       }
         sh 'docker push cbabu85/insure-me-app:1.0'
   }    
     }   
    stage('Application Deploy-container') {
          steps {
            
            ansiblePlaybook credentialsId: 'ubuntu-ssh', disableHostKeyChecking: true, installation: 'ansible', playbook: 'deploy.yml'
                }
          }
    }
}
