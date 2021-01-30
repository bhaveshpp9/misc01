pipeline {
  environment {
    imagename = "bhaveshpp9/misc01"
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
      steps {
	script {
	  dockerImage = docker.build imagename
      		}
	}

    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com' ,'git'  ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
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
