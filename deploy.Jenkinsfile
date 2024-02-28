pipeline {
    agent any

    parameters { string(name: 'ROBERTA_IMAGE_URL', defaultValue: '', description: '') }

    stages {
        stage('Deploy') {
            steps {
                sh 'echo $ROBERTA_IMAGE_URL'
            }
        }
    }
}
