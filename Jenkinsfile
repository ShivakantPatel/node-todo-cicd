pipeline {
    agent any
    stages {
        stage("code"){
            steps{
                git url: "https://github.com/ShivakantPatel/node-todo-cicd.git", branch: "master"
                echo 'code clone successfully'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t node-app-batch-6 ."
                echo 'code build successfully'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scan successfully'
            }
        }
        stage("push on docker"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app-batch-6:latest ${env.dockerHubUser}/node-app-batch-6:latest"
                sh "docker push ${env.dockerHubUser}/node-app-batch-6:latest"
                echo 'code push on docker successfully'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'deploy successfully'
            }
        }
    }
}
