pipeline {
    agent any

    stages {
        stage('Clone the Code') {
            steps {
                echo 'Cloning the code'
                git url:"https://github.com/Shahzad33/python-notes-app.git", branch:"main"
            }
        }
        stage('Build') {
            steps {
                echo 'Build the image'
                sh "docker build -t my-notes-app ."
            }
        }
        stage('Push the Docker Hub') {
            steps {
                echo 'Pushing the images Docker Hub'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "docker tag my-notes-app ${env.USERNAME}/my-notes-app:latest"
                    sh "docker login -u ${env.USERNAME} -p ${env.PASSWORD}"
                    sh "docker push ${env.USERNAME}/my-notes-app:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deployed the container'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

