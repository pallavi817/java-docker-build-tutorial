pipeline {
    agent { label 'slave1' }

    environment {
        DOCKERHUB = credentials('ntr1505-docker')
    }

    stages {
        stage('SCM Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/pallavi817/test6.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''docker build -t ntr1505/java:${BUILD_NUMBER} .'''
            }
        }

        stage('Login to DockerHub') {
            steps {
                sh '''echo $DOCKERHUB_PSW | docker login -u $DOCKERHUB_USR --password-stdin'''
            }
        }

        stage('Push Image') {
            steps {
                sh '''docker push ntr1505/java:${BUILD_NUMBER}'''
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
