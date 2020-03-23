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
                    sh "echo $DOCKER_IMAGE_NAME"
                    archiveArtifacts 'build.diff'
                    withEnv(["VAR=${println(diff)}"]){
                        echo "$VAR"
                    }
                    println(diff)
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
    post {
        always {
            slackSend channel: 'jenkins', message: "Build ${env.BUILD_NUMBER} completed for  ${env.JOB_NAME}.  Details: (<${env.BUILD_URL} | here >) ImageName: ${VAR}", teamDomain: 'homechat-crew', tokenCredentialId: 'slack_token' 
        }
    }    
}