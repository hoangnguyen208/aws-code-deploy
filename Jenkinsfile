pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/hoangnguyen208/aws-code-deploy.git'
            }
        }
        stage('Build stage') {
            steps {
                // This step should not normally be used in your script. Consult the inline help for details.
                withDockerRegistry(credentialsId: 'docker-hub', url: 'https://index.docker.io/v1/') {
                    // some block
                    sh 'docker build -t maestro021/test-jenkins:v1'
                    sh 'docker push maestro021/test-jenkins:v1'
                }
            }
        }
        stage('SSH server') {
            steps {
                sshPublisher(
                    continueOnError: false, failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: "remote-sv",
                            verbose: true,
                            transfers: [
                                sshTransfer(sourceFiles: "index.html")
                            ]
                        )
                    ]
                )
            }
        }
        post {
            always {
                mail bcc: '', body: 'Test Jenkins', cc: '', from: '', replyTo: '', subject: 'Test Jenkins', to: 'abc@gmail.com'
            }
        }
    }
}