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
          withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
        sh 'echo $PASS | docker login -u $USER --password-stdin'
        sh 'docker push kkushagra6/docker_argo_k8s:v$BUILD_ID'
          }      
        }
      }
    }

    stage('Checkout K8S manifest SCM'){
            steps {
                git credentialsId: 'c19209b1-238e-4b3e-8b35-d003594d568e', 
                url: 'https://github.com/kkushagra6/Jenkins_pipeline.git',
                branch: 'main'
            }
        }

    stage("Update the Image name in the k8s yaml that argo is watching") {
       steps{
         script{
           withCredentials([usernamePassword(credentialsId: 'c19209b1-238e-4b3e-8b35-d003594d568e', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
           sh '''
           echo "Testing"
           sed -i 's/docker_argo_k8s.*/docker_argo_k8s:v${BUILD_ID}/' ./deploy/deploy.yaml           
           git add .
           git commit -m "Updated Deploy YAML"
           git remote -v
           git push https://github.com/kkushagra6/Jenkins_pipeline.git HEAD:main
           '''
           }
         }
       } 
    }
    

  }
}
