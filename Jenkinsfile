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
                    writeFile file: 'build.diff', text: mostrecent_diff
                    emailext (
                      subject: "Sending diff of Job '${env.JOB_NAME} #${env.BUILD_NUMBER}'",
                      attachmentsPattern: '**/*.diff',
                      mimeType: 'text/html',
                      body: """<p>See attached diff of '${env.JOB_NAME} [${env.BUILD_NUMBER}]'.:</p>
                        <p>Check rich diff at <a href="${env.BUILD_URL}/last-changes">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
                      to: "loschmie@gmail.com"
                    
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
}