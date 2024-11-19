pipeline{
    agent {label "dev1-server"}
    stages{
        stage("code clone"){
            steps{
                git url: "https://github.com/PakeezaPakeeza/nodejs-todoapp-CICD.git", branch: "main"
            }
        }
        stage("code build and test"){
            steps{
                sh "docker build -t nodejs-notes-app ."
            }
        }
        stage("Push To DockerHub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerHubCreds",
                    usernameVariable:"dockerHubUser", 
                    passwordVariable:"dockerHubPass")]){
                sh 'echo $dockerHubPass | docker login -u $dockerHubUser --password-stdin'
                sh "docker image tag nodejs-notes-app:latest ${env.dockerHubUser}/nodejs-notes-app:latest"
                sh "docker push ${env.dockerHubUser}/nodejs-notes-app:latest"
                }
            }
        }
        stage("code deploy"){
            steps{
                sh "docker compose down && docker compose up -d --build"
            }
        }
    }
}
