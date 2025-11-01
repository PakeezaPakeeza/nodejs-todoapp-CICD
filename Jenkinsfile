pipeline{
    agent { label 'dev-server' };
    stages{
        stage("Code"){
            steps{
                echo "Code clone stage"
               git url: "https://github.com/PakeezaPakeeza/nodejs-todoapp-CICD.git", branch: "main"
               echo "code clone stage done" 
            }
        }
        stage("Build and test"){
            steps{
                
                echo "Code build stage"
                sh "whoami"
                sh "docker build -t notes-app ."
                echo "code build stage done"
            }
        }
        stage("Push to docker Hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCreds",
                    usernameVariable:"dockerHubUser", 
                    passwordVariable:"dockerHubPass")]){
                sh 'echo $dockerHubPass | docker login -u $dockerHubUser --password-stdin'
                sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app-2025:latest"
                sh "docker push ${env.dockerHubUser}/notes-app-2025:latest"
                }
            }
        }
        stage("scan image"){ 
            steps{ 
                echo 'I will add code in future' 
            } 
        } 
        stage("Deploy"){
            steps{
                sh "docker compose down && docker compose up -d --build"
                echo "code deploy stage done"
            }
        }
    }
}
