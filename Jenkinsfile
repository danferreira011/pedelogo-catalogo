pipeline{
    agent any

    stages{
        stage("Build Docker Image"){
            steps {
                script{
                    dockerapp = docker.build("danferreira011/api-produto:v${env.BUILD_ID}"), '-f ./src/PedeLogo.Catalogo.Api/Dockerfile ./src/PedeLogo.Catalogo.Api/ '
                }
            }
        }
        stage("Push Docker Image"){
            steps {
                script{
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                    dockerapp.push('latest')
                    dockerapp.push("v${env.BUILD_ID}")
                    }
                }
            }
        }
        stage("Deply no Kubernetes"){
            steps {
                sh 'echo "Executando Kubectl apply -f "'
            }
        }
    }
   

}
