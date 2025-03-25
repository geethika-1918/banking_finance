pipeline {
    agent any
    stages {
        stage('Checkout the Code from GitHub') {
            steps {
                git url: 'https://github.com/geethika-1918/banking_finance/'
                echo 'GitHub repository checked out'
            }
        }

        stage('Code Compilation') {
            steps {
                echo 'Starting compilation'
                sh 'mvn compile'
            }
        }

        stage('Code Testing') {
            steps {
                sh 'mvn test'
            }
        }

        stage('QA') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myimage .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'password', usernameVariable: 'username')]) {
                    sh 'echo "$password" | docker login -u "$username" --password-stdin'
                }
            }
        }

        stage('Tag and Push Docker Image') {
            steps {
                sh 'docker tag myimage geethikal03/myimage:latest'
                sh 'docker push geethikal03/myimage:latest'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -dt -p 8091:8091 --name c000 myimage'
            }
        }
    }
}
