@Library("Shared") _

pipeline{
    agent any;
    stages{
        stage("Code"){
            steps{
                script{
                clone ("https://github.com/Bahadur143/onlineshop-poc.git","dev")
                echo "Code clone successfully"
                }
            }
        }
        stage("Build"){
            steps{
                script{
                docker_build ("online-shop","latest","anilsahu350")
                echo "image build success fully"
                              }
                }
        }
        stage("Test"){
            steps{
                echo "Testing successfully"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                script{
                    docker_push("online-shop","latest","anilsahu350")
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
