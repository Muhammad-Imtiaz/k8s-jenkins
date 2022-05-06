// pipeline {

//   agent any
//   environment {
//     registry = "imtiaz1519/hello-world"
//     dockerImage = ""
//   }

//   stages {

//     stage('Checkout Source') {
//       steps {
//         git url:'https://github.com/Muhammad-Imtiaz/k8s-jenkins.git', branch:'master'
//       }
//     }

//     stage('Build image') {
//       steps{
//         script {
//           dockerImage = docker.build registry + ":latest"
//         }
//       }
//     }

//     stage('Push Image') {
//       steps{
//         script {
//           docker.withRegistry( "" ) {
//             dockerImage.push()
//           }
//         }
//       }
//     }


//     stage('Deploy App') {
//       steps {
//         script {
//           kubernetesDeploy(configs: "deployment.yaml", kubeconfigId: "mykubeconfig1")
//         }
//       }
//     }

//   }
// }

pipeline {

  agent any
  environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred')
	}

  stages {
  
    stage('Checkout Source') {
      steps {
        git url:'https://github.com/Muhammad-Imtiaz/k8s-jenkins.git', branch:'master'
      }
    }
        
    stage('Build') {

			steps {
				sh 'docker build -t imtiaz1519/hello-python:latest .'
			}
		}

		stage('Login') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push imtiaz1519/hello-python:latest'
			}
		}
   
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }
}

