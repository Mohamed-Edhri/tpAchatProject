pipeline {
    agent any 
    
    tools {
        maven 'mvn'
    }
    
    environment {
        imageName="backend-app"
        registryCredentials='nexus'
	registry ="/repository/my-jar-repo/"
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
                            //dockerImage = docker.build registry + ":$BUILD_NUMBER"
                            dockerImage = docker.build imageName
                       }
                 }
       }
        
               
         stage("Nexus Upload") {
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
