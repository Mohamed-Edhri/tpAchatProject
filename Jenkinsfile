pipeline {
    agent any 
    
    tools {
        maven 'mvn'
    }
    
    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "172.17.0.4:8081"
        NEXUS_REPOSITORY = "maven-releases"
        NEXUS_CREDENTIAL_ID = "nexus3"
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
        
        stage("SonarQube Analysis") {
          
           steps {
            withSonarQubeEnv('SonarQube') 
            {
                  sh ''' 
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=cidevops 
                        
                        '''
                  echo 'sonar static analysis done'
           }
           }
         }
                
        stage('maven package') {
             steps {
                  sh 'mvn package'
                  echo 'package done'
          }
       }
        
       stage("maven package") {
            steps {
                script {
                    echo "pulsihed to nexus done"
                       }
                  }
     }
        
     stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                    pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }
        
        post {
        always {
            emailext body: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS : Check console output at $BUILD_URL to view the results. ', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!'
        }
    }
   
}
}
