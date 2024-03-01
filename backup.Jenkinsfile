pipeline {
    agent any

    options {
        timestamps()
    }

    stages{
        stage('BackUp Jenkins') {
            steps {
                sh '''
                tar -czvf JenkinsBackUp.tar.gz --exclude=='caches' --exclude=='plugins' --exclude=='jobs' --exclude=='logs' --exclude=='workspace' $JENKINS_HOME/
                '''
            }
        }
        stage('Push to S3') {
            steps {
                sh 'aws s3 cp JenkinsBackUp.tar.gz s3://tamirmarzbuc/JenkinsBackUp.tar.gz'
            }
        }
    }
}