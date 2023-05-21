pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                sh 'docker build -t myflaskapp .'
            }
        }
        
        stage('Test') {
            steps {
                sh 'docker run myflaskapp python -m unittest'
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    sh 'docker tag myflaskapp bayanaltaleb/integrating_jenkins3:latest'
                    sh 'docker push bayanaltaleb/integrating_jenkins3:latest'
                }
            }
        }
    }
}