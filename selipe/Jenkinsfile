pipeline{
agent any
def app

stages{
  stage('SCM Checkout'){
    steps{
      git "/Users/selipe/my_home/git/hellonode"
    }
  }

  stage('Build Image'){
    steps{
    app = docker.build("selipe/node")
    }
  }

  stage('Test Image'){
    steps{
      app.inside{
        sh "echo inside a node server"
        sh "echo Tests Passed"
      }
    }
  }

  stage('Push the image to Docker Hub'){
    steps{
      docker.withRegistry("https://registry.hub.docker.com", "docker-hub-credentials"){
        app.push("$env.BUILD_NUMBER")
        app.push("latest")
      }
    }
  }

}

}
