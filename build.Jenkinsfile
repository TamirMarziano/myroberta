pipeline {
    agent any
    options {
        timestamps()
    }
    environment {
        ECR_URL = '352708296901.dkr.ecr.eu-central-1.amazonaws.com/tamirmarz-repo'
    }
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
                docker tag my-roberta $ECR_URL:my-roberta_$BUILD_NUMBER
                docker push $ECR_URL:my-roberta_$BUILD_NUMBER
                '''
            }
            post {
                always {
                    sh '''
                    docker image prune -a --force --filter "label=delete=false"
                    '''
                }
            }
        }
        stage('Trigger Deploy') {
            steps {
                build job: 'DeployRoberta', wait: false, parameters: [
                    string(name: 'ROBERTA_IMAGE_URL', value: "${ECR_URL}:my-roberta_${BUILD_NUMBER}")
                ]
            }
        }
        stage ('Clean workspace') {
            steps {
                cleanWs(cleanWhenNotBuilt: false,
                        deleteDirs: true,
                        disableDeferredWipeout: true,
                        notFailBuild: true,
                        patterns: [[pattern: '.gitignore', type: 'INCLUDE'],
                                    [pattern: '.propsfile', type: 'EXCLUDE']])
            }
        }
    }
}



