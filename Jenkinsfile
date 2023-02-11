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
                withEnv(["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"])
                {
                  sh 'docker login -u AWS -p $(aws ecr get-login-password --region us-east-1) 713884102309.dkr.ecr.us-east-1.amazonaws.com'
                  sh 'docker build -t apacheimage:${BUILD_NUMBER} . '
                  sh 'docker tag apacheimage:${BUILD_NUMBER} .'  
                   sh 'docker push 713884102309.dkr.ecr.us-east-1.amazonaws.com/my-registry::${BUILD_NUMBER}'  
               }
             } 
           }   
    }
}
