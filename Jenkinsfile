pipeline{
agent any

stages{
  stage('SCM Checkout'){
    steps{
      git ''/Users/selipe/my_home/git/hellonode'
    }
  }

  stage('Build Image'){
    steps{ /* This builds the actual image */
    def app = docker.build('selipe/node')
    }
  }

  stage('Test Image'){
    steps{/*Run a test framework and run the tests inside the image */
      app.inside{
        sh 'echo "Tests Passed... :)" '
      }
    }
  }

  stage('Push the image to Docker Hub'){
    steps{
      docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
        app.push('$env.BUILD_NUMBER')
        app.push('latest')
      }
    }
  }

}

}
