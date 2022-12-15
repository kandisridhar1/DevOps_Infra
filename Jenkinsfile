@Library('shared-library') _
pipeline {
    agent any
    
    environment {
       azcon = credentials('azure-pasha')
       }    
    stages {
      
      stage('Infra Provisioning') {
           when {
                expression { params.tfaction == "Infra" }
            }
           tools {
                   jdk "java"
                }
           steps {
               Infra()               
           }
           }
      stage('Infra Destroy') {
           when {
                expression { params.tfaction == "TerraformDestroy" }
            }
           tools {
                   jdk "java"
                }
           steps {
               TerraformDestroy()               
           }
           }
      stage('Run Containers') {   
           steps{
        
           withCredentials([usernamePassword(credentialsId: 'infravm', passwordVariable: 'password', usernameVariable: 'username')]) {
            RunInfraContainers(username, password)
            cleanWs()
        }
       
       }
       }
           }
           }
        
