pipeline {
    agent any

    parameters {
        booleanParam(name: 'deployToStaging', defaultValue: false, description: 'Deploy to Staging?')
        booleanParam(name: 'deployToProduction', defaultValue: false, description: 'Deploy to Production?')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build . -t node-app1'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run your tests (replace the command with your actual test command)
                    sh 'docker run --rm node-app1 npm test'
                }
            }
        }

        stage('Deploy to Staging') {
            when {
                expression { params.deployToStaging }
            }
            steps {
                script {
                    // Stop and remove existing Docker container
                    sh 'docker stop node-app1 || true'
                    sh 'docker rm node-app1 || true'

                    // Run Docker container for staging
                    sh 'docker run -d --name node-app1 -p 3000:3000 node-app1'
                }
            }
        }

        stage('Deploy to Production') {
            when {
                expression { params.deployToProduction }
            }
            steps {
                script {
                    // Stop and remove existing Docker container
                    sh 'docker stop node-app1 || true'
                    sh 'docker rm node-app1 || true'

                    // Run Docker container for production
                    sh 'docker run -d --name node-app1 -p 3000:3000 node-app1'
                }
            }
        }

        stage('Push to Registry') {
            steps {
                script {
                    // Login to Docker registry
                    sh 'echo "Aman*9261" | docker login -u "amanlaxkar" --password-stdin'

                    // Push Docker image to registry
                    sh 'docker push amanlaxkar/appimage:node-app1'
                }
            }
        }
    }
}
