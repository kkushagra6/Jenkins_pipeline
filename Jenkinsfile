pipeline{
  agent any

  stages{
    stage("Checkout"){
      steps{
        git credentialsId: 'c19209b1-238e-4b3e-8b35-d003594d568e',
        url: 'https://github.com/kkushagra6/Jenkins_pipeline.git',
        branch: 'main'
      }
    }
    stage("Docker") {
      steps{
      sh "docker build ."
      }


    }
  }

}
