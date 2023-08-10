
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
                sh 'docker build -t my-nginx-container .'
                sh 'docker run -p 80:80 my-nginx-container'
            }
        }
    }
}
