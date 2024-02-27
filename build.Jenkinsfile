pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t my-roberta .'
            }
        }
        stage('Push To ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 352708296901.dkr.ecr.eu-central-1.amazonaws.com
                docker tag my-roberta 352708296901.dkr.ecr.eu-central-1.amazonaws.com/tamirmarz-repo:my-roberta
                docker push 352708296901.dkr.ecr.eu-central-1.amazonaws.com/tamirmarz-repo:my-roberta
                '''
            }
        }
    }
}
