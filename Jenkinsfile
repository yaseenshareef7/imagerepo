pipeline {
environment {
registry = "yaseenshareef7/myregistry"
registryCredential = 'yaseenshareef7'
dockerImage = ''
}
agent any
stages {
stage('Cloning our Git') {
steps {
git 'https://github.com/yaseenshareef7/imagerepo.git'
}
}

