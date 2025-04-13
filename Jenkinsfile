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
                    // Build the Docker image based on your Dockerfile
                    dockerImage = docker.build("resume-analyzer-image")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop any existing containers with the same name (if any)
                    bat 'docker rm -f resume-analyzer-container || true'
                    // Run the container (For Windows)
                    bat 'docker run -d -p 8501:8501 --name resume-analyzer-container resume-analyzer-image'
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Optionally, clean up unused Docker images (to save space)
                    bat 'docker rmi resume-analyzer-image'
                }
            }
        }
    }
}
