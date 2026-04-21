pipeline{
    agent any

    stages{
        stage("Build Docker Image"){
            steps {
                script{
                    dockerapp = docker.build("danferreira011/api-produto:v${env.BUILD_ID}", '-f ./src/PedeLogo.Catalogo.Api/Dockerfile .')
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
        stage("Deploy no Kubernetes"){
            environment {
                tag_version = "${env.BUILD_ID}"
            }
            steps {
                // withKubeConfig([credentialsId: 'kubeconfig']) {
                withCredentials([[ $class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-credentials']]){
                  sh 'sed -i "s/{{tag}}/$tag_version/g" ./k8s/api.yaml' 
                  sh 'aws eks update-kubeconfig --region us-east-1 --name eks-devops'                 
                  sh 'kubectl apply -f k8s/'
                }
            }
        }
    }
   

}
