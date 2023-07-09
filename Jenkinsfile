pipeline{
  agent{
    docker {image 'docker/compose:debian-1.29.2'}
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
