pipeline {
    agent any 
    
    stages{
        stage("clone code from git"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/rameshawasthi/Jenkins.git", branch: "main"
            }
        }
        stage("Build the image"){
            steps {
                echo "Building the image"
                sh "docker build -t my-app ."
            }
        }
        stage("Push Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage("Deploy app"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
