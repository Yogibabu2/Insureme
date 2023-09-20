pipeline {
  agent any 
  tools {
     maven 'M2_HOME'
        }
stages {
     stage('Git Checkout') {
       steps {
         git 'https://github.com/Yogibabu2/Insureme.git'
             }
        }
  stage('Build Package') {
       steps {
         sh 'mvn package'
       }
     }
  
  stage('Publish HTML Reports') {
       steps {
         publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Insureme-Project/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
             }
         }
  stage('Create Docker image of App') {
       steps {
         sh 'docker build -t yogibaba1234/insure-me-app:3.0 .'
             }
         }
   stage('Docker Image Push') {
       steps {
         withCredentials([usernamePassword(credentialsId: 'docker1-hub', passwordVariable: 'docker_password', usernameVariable: 'docker_user')]) {
         sh 'docker login -u ${docker_login} -p ${docker_password}'
       }
         sh 'docker push yogibaba1234/insure-me-app:3.0'
             }    
       }   
}
}
