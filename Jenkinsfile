pipeline {   
  agent any 
  environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
    }
  stages {         
    stage("Git Checkout"){           
      steps{                
	checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yaseenshareef7/imagerepo.git']]])       //specifying git repo branch and creds in gui pipeline  ..       
	echo 'Git Checkout Completed'            
      }        
    }
      stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t myimage:${TAG} .' 
                  sh 'docker tag myimage yaseenshareef7/registry2:${TAG}'

               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "yaseenshareef7", url: "" ]) {
          sh  'docker push yaseenshareef7/registry2:${TAG}'
        
        }
                  
          }
     	 }
		 		 
   stage('Deploy'){
            steps {
                
                sh "docker run -d -p 9008:80 yaseenshareef7/registry2:${TAG}"
            }
        }
  }
}
