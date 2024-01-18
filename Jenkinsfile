pipeline {
    agent any
     tools{
        maven "M2_HOME"
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('vikramdochub')
        dockerHubUser='vikram2804'
        dockerHubPassword='vikram2804'
    }
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/vicky123-12/node-todo-cicd-master-jenkins.git', branch: 'master' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t vikram2804/node-todo-test:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	     sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push vikram2804/node-todo-test:latest'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
