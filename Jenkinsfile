<<<<<<< HEAD
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "banappanakattiganesh/dockerexp"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/bganesh-05/Docker.git'
                          
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:v1 .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(
                    credentialsId: 'dockerhub-PAT',
                    variable: 'DOCKER_PAT'
                )]) {
                    bat '''
                    @echo off
                    echo %DOCKER_PAT%|docker login -u banappanakattiganesh --password-stdin
                   if errorlevel 1 exit /b 1
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%:latest'
            }
        }
    }

    post {
        success {
            echo 'Docker image built and pushed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
=======
pipeline{
    agent any

    enviroment{
        DOCKER_IMAGE = "banappanakattiganesh/dockerexp"
    }

    stages{
        stage('Clone Repository') {
            steps{
                git 'https://github.com/bganesh-05/https://github.com/bganesh-05/Docker.git'
            }
        }

        stage('Build Docker Image'){
            steps{
                script{
                    docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }
        stage('Login to Docker Hub'){
             steps{
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }
        
        stage('Push Docker Image'){
            steps{
                script{
                    docker.withRegistry('','dockerhub-creds'){
                        docker.image("${DOCKER_IMAGE}:latest").push()
                    }
                }
            }
        }
    }
    post{
        success{
            echo 'Image successfully built and pushed to Docker Hub'
        }
        failure{
            echo 'Pipeline failed'
        }
    }
}
>>>>>>> 5f83f6ef419fccbc9457e07ccfb574d6da30d8f1
