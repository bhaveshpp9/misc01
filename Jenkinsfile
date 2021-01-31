pipeline {
  environment {
    imagename = "bparmar77/misc01"
    registryCredential = 'git'
    dockerImage = 'tomcat01'
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/bhaveshpp9/misc01.git', branch: 'master', credentialsId: 'f9153e19-b4f6-48b9-a773-e55a74cd294f'])

      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps{
        sh "sudo su - bhavesh; docker login; docker push bparmar77/misc01;"  
	}
     }    
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
          sh "docker rmi $imagename:latest"

      }
    }
  }
}
