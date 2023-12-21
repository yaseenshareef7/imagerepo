pipeline {
environment {
DOCKERHUB_CREDENTIALS = credentials('yaseenshareef7')
}
agent any
stages {
stage('Cloning our Git') {
steps {
git 'https://github.com/yaseenshareef7/imagerepo.git'
}
}
stage('Building our image') {
steps{
     sh 'docker build -t yaseenshareef7/myregitry:$BUILD_NUMBER .'
}
}
stage('login to dockerhub')
   steps{
       sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
stage('Deploy our image') {
steps{
     sh ' docker push yaseenshareef7/myregitry:$BUILD_NUMBER'
}
}
}
}
}
