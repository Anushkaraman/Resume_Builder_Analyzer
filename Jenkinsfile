pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Anushkaraman/Resume_Builder_Analyzer.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t smart-ai-resume-analyzer .'
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh 'docker stop resume-analyzer || true'
                    sh 'docker rm resume-analyzer || true'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh 'docker run -d -p 5000:5000 --name resume-analyzer smart-ai-resume-analyzer'
                }
            }
        }
    }
}
