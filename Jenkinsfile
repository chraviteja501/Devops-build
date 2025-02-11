pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './build.sh'
      }
    }
    stage('Push to Docker Hub') {
      steps {
        script {
          if (env.BRANCH_NAME == 'dev') {
            sh 'docker tag devops-build:latest <your-dockerhub-username>/dev:latest'
            sh 'docker push <your-dockerhub-username>/dev:latest'
          } else if (env.BRANCH_NAME == 'master') {
            sh 'docker tag devops-build:latest <your-dockerhub-username>/prod:latest'
            sh 'docker push <your-dockerhub-username>/prod:latest'
          }
        }
      }
    }
    stage('Deploy') {
      steps {
        sh './deploy.sh'
      }
    }
  }
}
