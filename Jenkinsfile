pipeline {
    agent any
    environment {
        //be sure to replace "willbla" with your own Docker Hub username
        DOCKER_IMAGE_NAME = "willbla/train-schedule"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'

            }
        }
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {


                }
            }
        stage('Push Docker Image') {
            when {
                branch 'master'
            }
            steps {
                echo 'Pushing the Image'

            }
        }
        stage('DeployToProduction') {
            when {
                branch 'master'
            }
            steps {
                echo 'deploying to Production'

            }
        }
    }
}