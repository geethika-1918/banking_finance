pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/geethika-1918/banking_finance/'
                 echo 'github url checkout'
            }
        }
        stage('codecompile'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('run dockerfile'){
          steps{
               sh 'docker build -t myimage .'
           }

          }
     stage('Login to Dockerhub') {
      steps {
             withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'password', usernameVariable: 'username')]) {
          // withCredentials([usernameColonPassword(credentialsId: 'docker-id-user', variable: 'docker-all')]) {
          // withCredentials([string(credentialsId: 'dockercode', variable: 'dockervarcode')]) {
           sh 'docker login -u geethikal03 -p ${password}'
                         }
                   }
               }        
    
     stage('Push the Docker image') {
      steps {
        sh 'docker push geethikal03/healthcare:latest'
                  }
            }
        stage('port expose'){
            steps{
                sh 'docker run -dt -p 8091:8091 --name c000 myimage'
            }
        }   
    }
}
