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
/*     stage('Build Package') {
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
         sh 'docker build -t cbabu85/insure-me-app:1.0 .'
             }
         }
     stage('Docker Image Push') {
       steps {
         withCredentials([usernamePassword(credentialsId: 'docker1-hub', passwordVariable: 'docker_password', usernameVariable: 'docker_user')]) {
         sh 'docker login -u ${docker_user} -p ${docker_password}'
       }
         sh 'docker push cbabu85/insure-me-app:1.0'
   }    
     }    */
    stage('Application Deploy-container') {
          steps {
            ansiblePlaybook become: true, credentialsId: 'SSH-Key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'prod.inv', playbook: 'deploy.yml'
                }
          }
    }
}
