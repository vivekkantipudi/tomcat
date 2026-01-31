pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/vivekkantipudi/tomcat.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop aditya || true
                docker rm aditya || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi thub || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t amazon .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 6060:8080 --name azure amazon'
            }
        }
    }
}
