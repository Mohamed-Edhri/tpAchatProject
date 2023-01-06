pipeline {
    agent any 
    
    tools {
        maven 'mvn'
    }
    
    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "192.168.1.90:8081"
        NEXUS_REPOSITORY = "maven-releases"
        NEXUS_CREDENTIAL_ID = "nexus3"
        imageName="myWebApp"
        registryCredentials='nexus'
	    registry ="http://192.168.1.90:8081/"
        dokerImage=''
    }
    
    stages {
        
        stage("Checkout GIT"){
            steps {
                git credentialsId: 'github' ,  url: 'https://github.com/Mohamed-Edhri/tpAchatProject.git'
                  }
        }
              
        stage ('maven clean') {
            steps {
                 sh 'mvn clean -e'
                 echo 'Build stage done'
                 }
       }
        
        stage("compile Project"){
        steps {
            sh 'mvn compile -X -e'
            echo 'compile stage done'
            }
        }
        
        stage("unit test"){
            steps {
                  sh 'mvn test'
                  echo 'unit tests stage done'
            }
        }
        
         stage("SonarQube Analysis") {
          
           steps {
            withSonarQubeEnv('SonarV9.7.1') 
            {
                  sh ''' 
                     mvn clean verify sonar:sonar \
                     -Dsonar.projectKey=devops-project
                  '''
                  echo 'sonar static analysis done'
           }
           }
         }
      
                        
        stage('maven package') {
             steps {
                  sh 'mvn package'
                  echo 'package done'
          }
       }
        
        
        stage("docker build") {
                       steps{
                         script {
                            //dockerImage = docker.build registry + ":$BUILD_NUMBER"
                            dockerImage = docker.build imageName
                       }
                 }
       }
        
        
        
         //  -------------- Upload Artifact to nexus ---------------
        
         stage('Uploading to Nexus') {
     steps{  
         script {
             docker.withRegistry( 'http://'+registry, registryCredentials ) {
             dockerImage.push('latest')
          }
        }
      }
    }
        
        
        
        
     
    }
}
