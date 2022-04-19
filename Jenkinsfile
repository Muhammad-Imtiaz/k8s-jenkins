pipeline {

  agent any
  environment {
    registry = "imtiaz1519/hello-world"
    dockerImage = ""
  }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/Muhammad-Imtiaz/k8s-jenkins.git', branch:'master'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":latest"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }


    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", kubeconfigId: "mykubeconfig1")
        }
      }
    }

  }
}
