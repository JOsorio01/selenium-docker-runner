pipeline {
    agent any
    stages {
        stage('Run Test') {
            steps {
                sh "docker-compose up"
            }
        }
        stage('Services down') {
            steps {
                sh "docker-compose down"
            }
        }
    }
}
