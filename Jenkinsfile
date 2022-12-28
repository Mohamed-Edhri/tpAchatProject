pipeline {
    agent any
     environment {
         JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
         M2_HOME="/opt/maven"
         MAVEN_HOME="/opt/maven"
         PATH="$PATH:/opt/maven/bin:"

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
