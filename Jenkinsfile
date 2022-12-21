pipeline {
    agent any
     environment {
         JAVA_HOME="/usr/lib/jvm/default-java"
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
        sh 'mvn clean'
        echo 'Build stage done'
           }
      }
        
    }
   
}
