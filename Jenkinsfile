pipeline {
    agent any 
    
    tools {
        maven 'mvn'
    }
    
    environment {
	    
	NEXUS_VERSION = "nexus2"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "192.168.1.90:8081"
        NEXUS_REPOSITORY = "maven-releases"
        NEXUS_CREDENTIAL_ID = "nexus"
        imageName="backend-app"
        dokerImage=''
    }
    
    stages {
        
        stage("GIT Cloning"){
            steps {
                git credentialsId: 'github' ,  url: 'https://github.com/Mohamed-Edhri/tpAchatProject.git'
                  }
        }
	 
	             
        stage ("MVN Clean") {
            steps {
                 sh 'mvn clean -e'
                 echo 'Build stage done'
                 }
       }
        
        stage("MVN Compile"){
        steps {
            sh 'mvn compile -X -e'
            echo 'compile stage done'
            }
        }
        
        stage("Unit Test"){
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
	    
	 
      
            
        stage("Docker Build") {
                       steps{
                         script {
                            dockerImage = docker.build imageName
                       }
                 }
       }
	    
        
               
         stage("Nexus Publisher") {
             steps{  
                 script {
                      nexusArtifactUploader artifacts: [[artifactId: 'spring-boot-maven', classifier: '', file: '/target/tpAchatProject-1.0.jar', type: 'jar']],
			      credentialsId: 'nexus', groupId: 'org.springframework.boot', 
			      nexusUrl: 'http://192.168.1.90:8081', 
			      nexusVersion: 'nexus2', protocol: 'http', 
			      repository: 'maven-releases', version: '1.0.0'  
                      }
                 }
        }
	    
    }  
}
