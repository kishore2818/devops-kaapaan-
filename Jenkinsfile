pipeline {
    agent any

    environment {
        PATH = "/opt/homebrew/bin:/usr/local/bin:${env.PATH}"
    }

    stages {

        stage('GitHub Check') {
            steps {
                sh 'pwd'
                sh 'ls -la'
                sh 'node -v || true'
                sh 'npm -v || true'
            }
        }

        stage('Frontend Build Test') {
            steps {
                dir('frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Backend Dependency Check') {
            steps {
                dir('backend') {
                    sh 'npm install'
                }
            }
        }

        stage('Docker Stop Old Containers') {
            steps {
                sh 'docker compose down || true'
            }
        }

        stage('Docker Build & Run') {
            steps {
                sh 'docker compose up --build -d'
            }
        }

        stage('Verify Running Containers') {
            steps {
                sh 'docker ps'
            }
        }

    }
}