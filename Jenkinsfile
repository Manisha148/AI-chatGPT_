pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t my-flask-app .'
            }
        }
        
        stage('Test') {
            
            steps {
                sh 'echo "Tests passed"'
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker tag my-flask-app $DOCKER_USERNAME/my-flask-app:latest'
                    sh 'docker push $DOCKER_USERNAME/my-flask-app:latest'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'docker run -p 8888:8888 manishaverma/my-flask-app:latest'
            }
        }
    }
}
