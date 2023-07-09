pipeline{
  agent{
    docker {image 'nginx:alpine'}
  }
  stages{
    stage("Docker") {
      steps{
      sh "docker-compose up -d"
      }
    }
    stage("Ran Successfully") {
      steps{
      sh 'docker ps -a'
      }
    }
  }
}
