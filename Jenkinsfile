pipeline {
    agent any
    stages {
        stage('Clone') {
            echo env.BRANCH_NAME
            steps {
                git 'https://github.com/hoangnguyen208/aws-code-deploy.git'
            }
        }
    }
}