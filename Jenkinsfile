pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build and Deploy') {
            steps {
                // Build the Docker image
                sh 'docker build -t nginx-web-server .'
                
                // Tag the Docker image
                sh 'docker tag nginx-web-server:latest brandonbudhram/nginx-web-server:v1.0'
                
                // Push the Docker image to the registry
                sh 'docker push brandonbudhram/nginx-web-server:v1.0'
                
                // You can also include the docker run command here if needed
            }
        }
    }
}

