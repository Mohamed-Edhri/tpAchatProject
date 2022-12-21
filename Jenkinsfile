pipeline {
    agent any
     environment {
        export JAVA_HOME=/usr/lib/jvm/default-java
        export M2_HOME=/opt/maven
        export MAVEN_HOME=/opt/maven
        export PATH=${M2_HOME}/bin:${PATH}
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
