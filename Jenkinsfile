pipeline {
    agent any
    stages {
        
        stage("Checkout GIT"){
            steps {
                git credentialsId: 'github' ,  url: 'https://github.com/Mohamed-Edhri/tpAchatProject.git'
           
            }
        }
        
        stage ('MVN clean') {
      steps {
        sh 'mvn clean -e'
        echo 'Build stage done'
      }
    }
        
        stage("compile Project"){
            steps {
                 sh 'mvn compile'
                  echo 'compile stage done'
            }
        }
        
       stage("maven tests"){
            steps {
                 sh 'mvn test'
                echo 'unit tests stage done'
            }
        }
        stage('Deploy') {
            steps {
                echo 'deploying the application...'
            }
        }
   
    }
}
