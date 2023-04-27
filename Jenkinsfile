pipeline {
    agent {label 'Dev'}
    
    stages {
        stage('Code'){
            steps {
                git url: 'https://github.com/amitkmr076/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build and Test'){
            steps {
                sh 'docker build . -t amitkmr076/node-todo-app:latest'
            }
        }
        stage('login and push Image'){
            steps {
                echo 'logging into Dockerhub and Push Image-'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerhubPassword', usernameVariable: 'dockerhubUser')]) {
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                    sh "docker push amitkmr076/node-todo-app:latest"
                }
            }
        }
        stage('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
