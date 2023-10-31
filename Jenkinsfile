pipeline {
    agent any

    stages {
        stage('Build and Deploy') {
            steps {
                script {
                    // Stop and remove existing Docker container
                    sh 'docker stop node-app1 || true'
                    sh 'docker rm node-app1 || true'

                    // Build Docker image
                    sh 'docker build . -t node-app1'

                    // Run Docker container
                    sh 'docker run -d --name node-app1 -p 3000:3000 node-app1'

                    // Login to Docker registry
                    sh 'echo "Aman*9261" | docker login -u "amanlaxkar" --password-stdin'

                    // Push Docker image to registry
                    sh 'docker push amanlaxkar/appimage:node-app1'
                }
            }
        }
    }
}
