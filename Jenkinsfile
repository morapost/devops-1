pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
        }
        stage('Upload to Nexus repo'){
            steps{
                 nexusArtifactUploader artifacts: [
                     [artifactId: 'simple-app', 
                      classifier: '', 
                      file: 'target/simple-app-1.0.0.war', 
                      type: 'war']
                 ], 
                     credentialsId: 'nexus3', 
                     groupId: 'bhush', 
                     nexusUrl: '3.236.21.41:8081', 
                     nexusVersion: 'nexus3', 
                     protocol: 'http', 
                     repository: 'jenkins-nexus', 
                     version: '1.0.0'
            }
        }
        }
    }
