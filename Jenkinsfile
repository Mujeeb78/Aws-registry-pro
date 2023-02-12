pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="713884102309"
        AWS_DEFAULT_REGION="us-east-1"
        IMAGE_REPO_NAME="my-registry"
        IMAGE_TAG="latest"
        REPOSITORY_URI = "713884102309.dkr.ecr.us-east-1.amazonaws.com/my-registry"
    }
   
    stages {
        
         stage('Logging into AWS ECR') {
            steps {
                script {
                sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 713884102309.dkr.ecr.us-east-1.amazonaws.com"
                }
            }
        }
        
  
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          sh "docker build -t my-registry ."
        }
      }
    }
   
    // Uploading Docker images into AWS ECR
    stage('Pushing to ECR') {
     steps{  
         script {
                sh "docker tag my-registry:latest 713884102309.dkr.ecr.us-east-1.amazonaws.com/my-registry:latest"
                sh "docker push 713884102309.dkr.ecr.us-east-1.amazonaws.com/my-registry:latest"
         }
        }
      }
    }
}
