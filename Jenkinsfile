pipeline {
    agent any
   
    environment {
        DOCKER_HUB_CREDENTIALS_ID = 'docker-hub-credentials'
    }
   
    stages {
        stage('Checkout') {
            steps {
                echo "Cloning"
                git url: "https://github.com/upadhyay02nitesh/django-notes-app.git", branch: "master"
            }
        }
       
        stage('Build') {
            steps {
                echo "Building the code"
                sh "docker build -t mynotes-app ."
            }
        }
       
        stage('Push To Docker Hub') {
            steps {
                echo "Push DockerHub"
                withEnv(["DOCKER_ACCESS_TOKEN=dckr_pat_eW5hzRKCiz74kdddtmBwjAWivco"]) {
                    sh "docker tag mynotes-app codeshop/mynotes-app:latest"
                    sh "docker login -u codeshop -p dckr_pat_eW5hzRKCiz74kdddtmBwjAWivco"
                    sh "docker push codeshop/mynotes-app:latest"
                }
            }
        }
       
        stage('Deploy') {
            steps {
                echo "Deploy to the server"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
