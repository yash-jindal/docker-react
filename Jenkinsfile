pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        DOCKER_IMAGE = 'yash/docker-react'
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE -f Dockerfile.dev .'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    sh 'docker run $DOCKER_IMAGE npm run test -- --coverage'
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
        }
    }
}
