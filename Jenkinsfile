pipeline{ /* +develop branch */
  agent any

  stages{
    stage('SCM Checkout'){
      steps{
      git "/Users/selipe/my_home/git/hellonode"
      }
    }

    stage('Build'){
      steps{
        script{
          def app = docker.build("selipe/node")
        }
        }
    }


    stage('Test'){
      when {
                branch 'release'
            }
        steps {
          script{
           app.inside {
              sh 'echo "Tests passed"'
           }
          }

          }
    }

    stage('Push it to Docker Hub'){
      when {
              branch 'master'
          }
          steps{
           script{
            /*def app = docker.build("selipe/node")*/
              docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
              app.push("$env.BUILD_NUMBER")
              app.push("latest")
      }

      }
    }
  }

}

}
