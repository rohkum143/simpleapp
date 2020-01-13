pipeline {
  environment {
  registry = "rohtashkumar/nginxdemo"
  registryCredential = "dockerhub_1"
  dockerImage = ""
  }
agent any
 stages {
  stage('Building image') {
   steps{
    script {
      dockerImage = docker.build registry
      sh 'echo "rohtashkumar/nginxdemo" > anchore_images'
      sh 'ls -ltra'
    }}}
  stage('Security') {
    steps {
     anchore name: 'anchore_images'
    }}
  stage('Deploy Image') {
   steps{
    script {
      docker.withRegistry( '', registryCredential ) {
      dockerImage.push()
   }}}}
    stage('Cleanup') {
   steps {
   sh'''
     for i in `cat anchore_images | awk ‘{print $1}’`;do docker rmi $i; done
   '''}}}}
