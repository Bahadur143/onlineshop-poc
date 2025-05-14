pipeline{
    agent any;
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/Bahadur143/onlineshop-poc.git",branch:"dev"
                echo "Code clone successfully"
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t online-shop -f ./Dockerfile-multi ."
                echo "image build success fully"
                }
        }
        stage("Test"){
            steps{
                echo "Testing successfully"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHubCred",
                passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker image tag online-shop:latest ${env.dockerHubUser}/online-shop:latest"
                    sh "docker push ${env.dockerHubUser}/online-shop:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d "
            }
        }
    }
}
