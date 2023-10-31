pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    sh 'docker build . -t node-app1'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh 'docker run --rm node-app1 npm test'
                }
            }
        }

        stage('Code Quality') {
            steps {
                script {
                    sh 'docker run --rm -v $PWD:/app -w /app node-app1 npm run lint'
                }
            }
        }

        stage('Approval') {
            steps {
                script {
                    // Assuming you want automatic approval if the previous stages were successful
                    // You can customize this condition based on your requirements
                    if (currentBuild.resultIsBetterOrEqualTo('SUCCESS')) {
                        echo 'Automatic approval - Build, Test, and Code Quality stages passed'
                    } else {
                        error 'Build, Test, or Code Quality stages failed. Manual approval required.'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'docker stop node-app1 || true'
                    sh 'docker rm node-app1 || true'
                    sh 'docker run -d --name node-app1 -p 3000:3000 node-app1'
                }
            }
        }

        stage('Push to Registry') {
            steps {
                script {
                    sh 'echo "Aman*9261" | docker login -u "amanlaxkar" --password-stdin'
                    sh 'docker push amanlaxkar/appimage:node-app1'
                }
            }
        }
    }
}
