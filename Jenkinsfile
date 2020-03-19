pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "loschmie/train-schedule"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Running some crazy shit'
            }
        }
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                echo 'Building Docker Image'
                }
            }
        }

        stage('DeployToProduction') {
            when {
                branch 'master'
            }
            steps {
                input 'Deploy to Production?'
                milestone(1)
                echo 'app deployed!'
            }
        }
    }
}