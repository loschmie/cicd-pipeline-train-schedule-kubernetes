pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "loschmie/testing_test"
    }
    stages {
        stage('Get Bild Diff') {
            steps {
                script {
                    def publisher = LastChanges.getLastChangesPublisher null, "SIDE", "LINE", true, true, "", "", "", "", ""
                    publisher.publishLastChanges()
                    def changes = publisher.getLastChanges()
                    def diff = changes.getDiff()
                    writeFile file: 'build.diff', text: diff
                    archiveArtifacts 'build.diff'
                }
                
            }
        }

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
                    echo 'Building docker image ${DOCKER_IMAGE_NAME}"'
                }
            }
        stage('Push Docker Image') {
            when {
                branch 'master'
            }
            steps {
                echo "Pushing image"
               
            }

        }

    }
    post {
        always {
            script {
                def data = readFile(file: 'build.diff').trim()
                slackSend channel: 'jenkins', message: "Build ${env.BUILD_NUMBER} completed for  ${env.JOB_NAME}.  Bild diff: ${data}", teamDomain: 'homechat-crew', tokenCredentialId: 'slack_token'
            }
             
        }
    }    
}