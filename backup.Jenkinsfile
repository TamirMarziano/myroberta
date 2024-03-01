pipeline {
    agent any

    options {
        timestamps()
    }

    stages{
        stage('BackUp Jenkins') {
            steps {
                sh '''
                tar -czvf JenkinsBackUp.tar.gz --exclude==$JENKINS_HOME/caches --exclude==$JENKINS_HOME/plugins --exclude==$JENKINS_HOME/jobs --exclude==$JENKINS_HOME/logs --exclude==$JENKINS_HOME/workspace $JENKINS_HOME
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