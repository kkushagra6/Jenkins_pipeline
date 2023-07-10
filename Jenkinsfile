pipeline{
  agent any


  stages{
    
    stage("Docker Build") {
      steps{
      sh "docker build -t kkushagra6/docker_argo_k8s:v$BUILD_ID ."
      }
    }
    stage("Docker Authenticate & Push to repo") {
      steps{
        script{
          withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')])' {
        sh 'echo $PASS | docker login -u $USER --password-stdin'
        sh 'docker push kkushagra6/docker_argo_k8s:v$BUILD_ID'
          }      
        }
      }
    }
    stage("Update the Image name in the k8s yaml that argo is watching") {
       steps{
       echo "Testing"
       }
    }
    

  }
}
