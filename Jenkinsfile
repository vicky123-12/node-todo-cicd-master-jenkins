pipeline {
    agent any
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
                withCredentials([usernamePassword(credentialsId: 'vikramdochub', passwordVariable: 'vikramdochubPassword', usernameVariable: 'vikramdochubUser')]) {
        	     sh "docker login -u ${env.vikramdochubUser} -p ${env.vikramdochubPassword}"
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
