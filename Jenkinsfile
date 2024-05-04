pipeline {
    agent any
    environment{
        IMAGE_NAME = "fponzio31/python-app"
        DOCKERHUB_CREDS = credentials('dockerhub')
    }

    stages {
        stage('Build image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
            }
        }
        stage("Docker login"){
            steps{
                sh 'echo ${DOCKERHUB_CREDS_PSW} | docker login -u ${DOCKERHUB_CREDS_USR} --password-stdin'
            }
        }

        stage("Docker push"){
            steps{
                sh 'docker push ${IMAGE_NAME}:${BUILD_NUMBER}'
            }
        }
    }
        post {
            always {
                sh 'docker logout'
            }
        }  
        
}

