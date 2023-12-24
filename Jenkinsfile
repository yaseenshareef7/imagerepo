pipeline {   
  agent any  
  stages {         
    stage("Git Checkout"){           
      steps{                
	checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yaseenshareef7/imagerepo.git']]])       //specifying git repo branch and creds in gui pipeline  ..       
	echo 'Git Checkout Completed'            
      }        
    }
      stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t myimage:1.2 .' 
                  sh 'docker tag myimage yaseenshareef7/myregistry:1.2'

               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "yaseenshareef7", url: "" ]) {
          sh  'docker push yaseenshareef7/myregistry:1.2'
        
        }
                  
          }
     	 }
		 		 
   stage('Deploy'){
            steps {
                
                sh "docker run --name myngninx-image -d -p 9004:80 yaseenshareef7/myregistry:1.2"
            }
        }
  }
}
