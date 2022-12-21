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
        
      
   
    }
}
