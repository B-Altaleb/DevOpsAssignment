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
                // Checkout source code from version control
                sh 'docker build -t integrating_jenkins77 .'
            }
        }
        
        stage('Test') {
            steps {
                sh 'docker run integrating_jenkins77 python -m unittest'
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                sh 'docker tag integrating_jenkins5 $DOCKER_USERNAME/integrating_jenkins77'
                sh 'docker push $DOCKER_USERNAME/integrating_jenkins77'
            }
        }
    }
}
