#!/usr/bin/env groovy

pipeline {
    agent any

    stages {
        stage('In this stage we will clone the repository using the main branch.') {
            steps {
                git branch: 'main', url: 'https://github.com/brandonbudhram00/DevOPS-'
            }
        }

        stage('In this stage we will build the image using the dockerfile in the github') {
            steps {
                script {
                    def dockerImage = docker.build("brandonbudhram/web-app:${env.BUILD_ID}", "-f Dockerfile .")
                    env.IMAGE_NAME = "brandonbudhram/web-app:${env.BUILD_ID}"
                }
            }
        }

        stage('In this stage we will push the dockerfile to dockerhub') {
            environment {
                DOCKER_HUB_USERNAME = 'brandonbudhram'
                DOCKER_HUB_REPOSITORY = 'web-app'
                DOCKER_HUB_PASSWORD = '347tripledouble012?'
            }
            steps {
                script {
                    sh "docker tag ${env.IMAGE_NAME} ${DOCKER_HUB_USERNAME}/${DOCKER_HUB_REPOSITORY}:${env.BUILD_ID}"
                    sh "docker tag ${env.IMAGE_NAME} ${DOCKER_HUB_USERNAME}/${DOCKER_HUB_REPOSITORY}:latest"
                }
                sh "docker login -u ${DOCKER_HUB_USERNAME} -p ${DOCKER_HUB_PASSWORD}"
                sh "docker push ${DOCKER_HUB_USERNAME}/${DOCKER_HUB_REPOSITORY}:${env.BUILD_ID}"
                sh "docker push ${DOCKER_HUB_USERNAME}/${DOCKER_HUB_REPOSITORY}:latest"
            }
        }

        stage('In this stage we will run the docker container on port 80') {
            steps {
                script {
                    sh "docker run -p 80:80 -d --name web-app ${env.IMAGE_NAME}"
                }
            }
        }
    }
}

