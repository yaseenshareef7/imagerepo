pipeline {   
  agent any
  environment {     
    DOCKERHUB_CREDENTIALS= credentials('yaseenshareef7')     
  }    
  stages {         
    stage("Git Checkout"){           
      steps{                
	git credentialsId: '2aa7e006-56ec-4189-ae08-ca53dc41bd30', url: 'https://github.com/yaseenshareef7/imagerepo.git'                 
	echo 'Git Checkout Completed'            
      }        
    }
    stage('Build Docker Image') {         
      steps{                
	sh 'sudo docker build -t yaseenshareef7/myregistry:$BUILD_NUMBER .'           
        echo 'Build Image Completed'                
      }           
    }
    stage('Login to Docker Hub') {         
      steps{                            
	sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                 
	echo 'Login Completed'                
      }           
    }               
    stage('Push Image to Docker Hub') {         
      steps{                            
	sh 'sudo docker push yaseenshareef7/myregistry:$BUILD_NUMBER'                 echo 'Push Image Completed'       
      }           
    }      
  } //stages 
  post{
    always {  
      sh 'docker logout'           
    }      
  }  
} //pipeline
