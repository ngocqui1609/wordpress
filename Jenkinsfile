pipeline {
   agent any
    stages {
    stage("build") {
      
      environment {
        IMAGE_TAG="${GIT_BRANCH.tokenize('/').pop()}-${GIT_COMMIT.substring(0,7)}"
      }
      steps {
        script {
          sh 'docker build -t ${REPOSITORY_URI}:${IMAGE_TAG} . '
          sh 'docker stop ${IMAGE_REPO_NAME}'
          sh 'docker rm ${IMAGE_REPO_NAME}'
          sh 'docker rmi ${REPOSITORY_URI}:latest'          
          sh 'docker tag ${REPOSITORY_URI}:${IMAGE_TAG} ${REPOSITORY_URI}:latest'
          sh 'docker image ls | grep ${IMAGE_REPO_NAME}'
          // sh 'aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com'
          // sh 'docker push ${REPOSITORY_URI}:${IMAGE_TAG}'
          // sh 'docker push ${REPOSITORY_URI}:latest'
          //clean to save disk
          sh 'docker image rm ${REPOSITORY_URI}:${IMAGE_TAG}'
          // sh 'docker image rm ${REPOSITORY_URI}:latest'
          sh 'docker rm $(docker ps --filter status=exited -q)'
          sh 'docker rmi $(docker images -q -f dangling=true)'
          // sh 'docker system prune --all --force'
        }
      }
    }
    stage("deploy") {
      
      steps {
        script {
          // sh 'aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com'
          // sh 'docker stop ${IMAGE_REPO_NAME}'
          // sh 'docker rm ${IMAGE_REPO_NAME}'
          // sh 'docker rmi ${REPOSITORY_URI}'
          sh 'docker run -it -d -p 80:3000 --name ${IMAGE_REPO_NAME} ${REPOSITORY_URI}:latest'
        } 
      }
    }  
  }

  post {
    success {
      echo "SUCCESSFUL"
    }
    failure {
      echo "FAILED"
      
    }
  }
}
