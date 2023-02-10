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
                sh 'docker build -t apacheimage . '
                sh 'docker images'
            }
        }
        stage('Tag and push Docker image to AWSRegistry') {
            steps {
            
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 713884102309.dkr.ecr.us-east-1.amazonaws.com'
                sh 'docker tag my-registry:latest 713884102309.dkr.ecr.us-east-1.amazonaws.com/my-registry:latest'
                sh 'docker push 713884102309.dkr.ecr.us-east-1.amazonaws.com/my-registry:latest'
                
                }
                
                }
        
        
    }
}
