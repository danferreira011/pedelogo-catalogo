pipeline{
    agent any

    stages{
        stage("Build Docker Image"){
            steps {
                sh 'echo "Executando Docker Build"'
            }
        }
        stage("Push Docker Image"){
            steps {
                sh 'echo "Executando Docker Push"'
            }
        }
        stage("Deply no Kubernetes"){
            steps {
                sh 'echo "Executando Kubectl apply -f "'
            }
        }
    }
   

}
