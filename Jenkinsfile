pipeline {
    agent any
     environment {
         JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
         M2_HOME="/opt/maven"
         MAVEN_HOME="/opt/maven"
         PATH="${M2_HOME}/bin:${PATH}"

     }
    
    stages {
        
        stage("Checkout GIT"){
            steps {
                git credentialsId: 'github' ,  url: 'https://github.com/Mohamed-Edhri/tpAchatProject.git'
                  }
        }
        
        stage ('maven clean') {
            steps {
                 sh 'mvn clean install'
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
         
        stage('maven package') {
             steps {
               sh 'mvn package'
          }
       }
        
    }
   
}
