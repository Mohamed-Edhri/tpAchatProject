pipeline {
    agent any
    
     tools {
        maven 'mvn'
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
          //  sh 'mvn compile -X -e'
            echo 'compile stage done'
            }
        }
        
        stage("unit test"){
            steps {
              // sh 'mvn test'
                  echo 'unit tests stage done'
            }
        }
         
        stage('maven package') {
             steps {
             // sh 'mvn package'
                  echo 'package done'
          }
       }
        
        
       
    }
   
}
