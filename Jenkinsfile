pipeline{
  agent any

  stages{
    stage('SCM Checkout'){
      steps{
      git "/Users/selipe/my_home/git/hellonode"
      }
    }

/**
*    stage('Build Image'){
*     steps{
*       script {
*        def app = docker.build("selipe/node")
*       }
*      }
*    }
**/


   stage('Build and Push the image to Docker Hub'){
    steps{
      script{
        def app = docker.build("selipe/node")
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
          app.push("$env.BUILD_NUMBER")
          app.push("latest")
      }

      }
    }
  }

}

}
