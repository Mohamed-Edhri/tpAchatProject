pipeline {
    agent any 
    
    tools {
        maven 'mvn'
    }
    
    environment {
	    
	NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "192.168.1.90:8081"
        NEXUS_REPOSITORY = "maven-snapshots"
        NEXUS_CREDENTIAL_ID = "nexus"
	registry="mimo20222/edhri2023_docker_hub_repo"
        registryCredential='docker-hub-id'
        imageName="webapp"
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
                           // dockerImage = docker.build imageName
		               dockerImage = docker.build registry + imageName
                       }
                 }
       }
	    
	    stage(" DockerHub Push ") {
              steps{
                 script {
                 docker.withRegistry( '', registryCredential ) 
				        {
                          //dockerImage.push()
                          sh 'docker tag imageName mimo20222/edhri2023_docker_hub_repo:webapp-1.0'
			  sh 'docker push mimo20222/edhri2023_docker_hub_repo:webapp-1.0'
                        }
                }
             }
        }

	 //stage("Publish to Nexus") {
         //   steps {
           //     script {
                       //nexusPublisher nexusInstanceId: 'maven-releases', nexusRepositoryId: '', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '\\target\\tpAchatProject-1.0.jar']], mavenCoordinate: [artifactId: 'spring-boot-maven-plugin', groupId: 'org.springframework.boot', packaging: 'jar', version: '1.0']]]
          //            nexusArtifactUploader artifacts: [[artifactId: 'spring-boot-maven-plugin', classifier: '', file: 'target/tpAchatProject-1.0.jar', type: 'jar']], credentialsId: 'nexus', groupId: 'org.springframework.boot', nexusUrl: '192.168.1.90:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0'
		  //     }
       //            }
      //    }
	    
        
               
        
	    
    }  
}

