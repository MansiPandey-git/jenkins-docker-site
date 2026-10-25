
pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-docker-site:latest .'
            }
        }

        stage('Deploy Website') {
            steps {
                sh '''
                    docker rm -f jenkins-docker-site || true
                    docker run -d --restart unless-stopped \
                        --name jenkins-docker-site \
                        -p 80:80 jenkins-docker-site:latest
                '''
            }
        }
    }
}
