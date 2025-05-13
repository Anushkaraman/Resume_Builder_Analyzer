pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "resume-analyzer-image"
        DOCKER_CONTAINER = "resume-analyzer-container"
        PORT = "8501"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Anushkaraman/Resume_Builder_Analyzer.git'
            }
        }
        stage('Remove Old Container and Image') {
            steps {
                echo '=== Stopping and Removing Old Container ==='
                bat "docker stop resume-analyzer-container || echo Container not running"
                bat "docker rm resume-analyzer-container || echo Container not found"
                echo '=== Removing Old Docker Image ==='
                bat "docker rmi resume-analyzer-image || echo Image not found or in use"
            }
        }
        stage('Build Docker Image') {
            steps {
                echo '=== Building New Docker Image ==='
                bat "docker build -t resume-analyzer-image ."
            }
        }
        stage('Run Docker Container') {
            steps {
                echo '=== Running New Container ==='
                bat "docker run -d -p 8501:8501 --name resume-analyzer-container resume-analyzer-image"
            }
        }
    }
}
