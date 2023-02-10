pipeline {
    agent any
    stages {
        stage("Checking Docker Version") {
            steps {
                retry(3){
                sh "docker --version"
                }
            }
        }
        stage("Checking GIT Version") {
            steps {
                sh "git --version"
            }
        }
        stage('Build Docker Image with build no') {
            steps {
                sh 'docker build -t apacheimage:${BUILD_NUMBER} . '
                sh 'docker images'
            }
        }
        stage('Tag and push Docker image to AWSRegistry') {
            steps {
                withCredentials('credentialsId: ecr:us-east-1:f9bd1cb4-5dcf-44fb-a128-2588ca4e9ae9')
                {
                docker tag apacheimage${BUILD_NUMBER}:latest 713884102309.dkr.ecr.us-east-1.amazonaws.com/my-registry:$BUILD_NUMBER
                docker push 713884102309.dkr.ecr.us-east-1.amazonaws.com/my-registry:$BUILD_NUMBER
                }
                
                }
        }
        
    }
}
