pipeline {
    agent any
	
	  tools
    {
       maven "M2_HOME"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/Annamalaipts98/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp annamalaipts/samplewebapp:latest'
                //sh 'docker tag samplewebapp annamalaipts/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
 stage('Publish image to Docker Hub') {
          
          steps {
          withDockerRegistry([ credentialsId: "dockerhub_id", url: "" ]) {
          sh  'docker push annamalaipts/samplewebapp:latest'
          //sh  'docker push annamalaipts/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 annamalaipts/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.7.140 run -d -p 8003:8080 annamalaipts/samplewebapp"
 
            }
        }
    }
	}
    
