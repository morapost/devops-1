  
pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    options {
      buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
        }
        stage('Upload to Nexus repo'){
            steps{
                script {
                        def pomVersion = readMavenPom file: 'pom.xml'
                        def nexusRepoName = pomVersion.version.endsWith("SNAPSHOT") ? "jenkins-nexus-snapshot" : "jenkins-nexus"
                        nexusArtifactUploader artifacts: [
                         [artifactId: 'simple-app', 
                          classifier: '', 
                          file: "target/simple-app-${pomVersion.version}.war", 
                          type: 'war']
                     ], 
                         credentialsId: 'nexus3', 
                         groupId: 'bhush', 
                         nexusUrl: '3.236.21.41:8081', 
                         nexusVersion: 'nexus3', 
                         protocol: 'http', 
                          repository: "${nexusRepoName}", 
                         version: "${pomVersion.version}"
                }
            }    
        }
    }
}
