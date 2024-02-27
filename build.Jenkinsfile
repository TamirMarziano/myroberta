pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t my-roberta .'
            }
        }
    }
        stage('Push To ECR') {
            steps {
                sh '''
                docker tag my-roberta 352708296901.dkr.ecr.eu-central-1.amazonaws.com/tamirmarz-repo:my-roberta
                docker push 352708296901.dkr.ecr.eu-central-1.amazonaws.com/tamirmarz-repo:my-roberta
                '''
            }
        }
    }
}