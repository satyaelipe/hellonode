def app
pipeline{ /* +develop branch */
  agent any

  stages{
    stage('SCM Checkout'){
      steps{
      /*git "/Users/selipe/my_home/git/hellonode"*/
        // git "https://github.com/selipe16474/hellonode.git"
        git 'https://github.com/satyaelipe/hellonode.git'
      }
    }

    stage('Build'){
      steps{
        script{
          app = docker.build("selipe/node")
          println "from Build"
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
              println "Tests passed"
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
           println "from push"
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
