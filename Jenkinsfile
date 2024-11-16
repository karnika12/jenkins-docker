pipeline {
    agent { label 'slave' }  // Use agent label as specified
    
    environment {
        IMG_NAME = 'my-nx'
        AWS_REGION = 'us-east-1'  // Updated region to us-east-1
        ECR_URI = '783764595862.dkr.ecr.us-east-1.amazonaws.com/test/docker'  // Your ECR URI
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t ${IMG_NAME} .'
                    
                    // Tag the image for ECR push
                    sh 'docker tag ${IMG_NAME} ${ECR_URI}:latest'
                }
            }
        }
        
        stage('Login to AWS ECR') {
            steps {
                withCredentials([aws(credentialsId: 'AWS-Credentials', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    script {
                        // Authenticate Docker to AWS ECR using AWS CLI
                        sh '''
                            aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ECR_URI}
                        '''
                    }
                }
            }
        }

        stage('Push to ECR') {
            steps {
                script {
                    // Push the Docker image to ECR
                    sh 'docker push ${ECR_URI}:latest'
                }
            }
        }
    }
}
