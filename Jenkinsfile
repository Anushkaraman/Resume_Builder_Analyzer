pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Anushkaraman/Resume_Builder_Analyzer.git' // Update with your GitHub repo URL
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
                    sh 'docker rm -f resume-analyzer-container || true'
                    
                    // Run the container
                    sh 'docker run -d -p 8501:8501 --name resume-analyzer-container resume-analyzer-image'
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Optionally, clean up unused Docker images (to save space)
                    sh 'docker rmi resume-analyzer-image'
                }
            }
        }
    }
}
