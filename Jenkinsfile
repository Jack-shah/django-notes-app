pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/LondheShubham153/django-notes-app.git']])
            }
        }
        stage('docker build') {
            steps {
               echo 'building  the image'
               sh '''
                    whoami   
                    docker build -t awajid980/project1:1.0 .
               '''
            }
        }
        stage('docker push') {
            steps {
                echo 'push image to docker hub or any artifactory'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dpass', usernameVariable: 'duser')]) 
                {
                sh "docker login -u ${env.duser} -p ${env.dpass}"
                sh "docker push awajid980/project1:1.0"
                }
            }
        }
        stage('deploy ') {
            steps {
                //sh"docker run -d -p 8000:8000 awajid980/project1:1.0"     
                sh"docker-compose down && docker-compose up"
            }
        }
    }
}
