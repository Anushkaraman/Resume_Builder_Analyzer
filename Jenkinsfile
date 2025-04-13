pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Anushkaraman/Resume_Builder_Analyzer.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo '=== Building Docker Image ==='
                    dockerImage = docker.build("resume-analyzer-image")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    echo '=== Removing old container ==='
                    bat 'docker rm -f resume-analyzer-container 2>nul'

                    echo '=== Running container ==='
                    bat 'docker run -d -p 8501:8501 --name resume-analyzer-container resume-analyzer-image'
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    echo '=== Optional Cleanup of Image ==='
                    bat 'docker rmi resume-analyzer-image'
                }
            }
        }
    }
}
