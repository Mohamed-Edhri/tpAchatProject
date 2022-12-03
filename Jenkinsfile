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
                 sh 'mvn compile -X -e'
                  echo 'compile stage done'
            }
        }
        
       stage("Build") { 
            steps { 
                echo  'building the application...' 
            }
        }
        stage("Test"){
            steps {
                echo 'testing the application...'
                
            }
        }
        stage('Deploy') {
            steps {
                echo 'deploying the application...'
            }
        }
   
    }
}
