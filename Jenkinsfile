pipeline {
    agent any
    environment {
        //be sure to replace "willbla" with your own Docker Hub username
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
                    BUILD_DIFF = echo "$diff"
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
                echo "UPloading this shit"
            }

        }

    }
    post {
        always {
            slackSend channel: 'jenkins', message: "Build ${env.BUILD_NUMBER} completed for  ${env.JOB_NAME}.  Details: ${BUILD_DIFF}", teamDomain: 'homechat-crew', tokenCredentialId: 'slack_token' 
        }
    }    
}