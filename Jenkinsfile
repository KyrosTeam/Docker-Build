pipeline {
  agent { label 'docker' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  triggers {
    cron('@daily')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -f "Dockerfile-terraform" -t brightbox/terraform:latest .'
        sh 'docker build -f "Dockerfile-cli" -t brightbox/cli:latest .'
      }
    }
    stage('Publish') {
      when {
        branch 'master'
      }
      steps {
        withDockerRegistry([ credentialsId: "	dockerhub", url: "https://cloud.docker.com/u/vishnuprasadnarayanan/repository/docker/vishnuprasadnarayanan/docker_images" ]) {
          sh 'docker push brightbox/terraform:latest'
          sh 'docker push brightbox/cli:latest'
        }
      }
    }
  }
}
