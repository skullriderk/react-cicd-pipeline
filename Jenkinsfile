pipeline {
    agent any

    stages {
        stage('code pull') {
            steps {
                // Get code from a GitHub repository
                git 'https://github.com/skullriderk/react-cicd-pipeline.git'
            }
        }
          stage('Docker image') {
            steps {
                // build docker image
               sh 'docker build -t react:v${BUILD_NUMBER} .'
            }
        }
    stage('Docker container') {
            steps {
                // build docker container
                sh 'docker stop Reactapp || true'
                sh 'docker rm Reactapp || true'
               sh 'docker run -d --name Reactapp -p 8081:3000 react:v${BUILD_NUMBER}'
            }
        }
    }
}
