pipeline{
    agent any
    tools{
     maven 'maven3'
     }
     stages{
         stage('build maven'){
             steps{
                 checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/amdadul1994/java-apps-automation']]])
                 sh 'mvn clean install'  
             }
            }
         stage('docker build'){
             steps{
                script{
                   sh 'docker build -t himu1994/java-apps-automation .'
                }
             }
            }
         stage('docker hub push'){
             steps{
                script{
                   withCredentials([string(credentialsId: 'docker-secret', variable: 'dockerlogin')]) {
                   sh 'docker login -u himu1994 -p ${dockerlogin}'  
                } 
                   sh 'docker push himu1994/java-apps-automation'
                }
             }
            }
    }
}