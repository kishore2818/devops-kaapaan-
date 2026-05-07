
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

        stage('Create Backend Env') {
            steps {
                writeFile file: 'backend/.env', text: '''
PORT=5000
CRM_PORT=4000





MONGO_URI=mongodb+srv://nt03625:mzRewbYxcaNBVX3A@clusterdb.ycdxi.mongodb.net/traffic_violation?retryWrites=true&w=majority

CLOUDINARY_CLOUD_NAME=ddg5ao8e7
CLOUDINARY_API_KEY=282649857566918
CLOUDINARY_API_SECRET=jpQvjZaCPHhf29KZE2-UM0NTm4U

FRONTEND_URL=http://localhost:3000
'''
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