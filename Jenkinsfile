pipeline{

  agent any

  stages{
    stage('SCM Checkout'){
      steps{
      git "/Users/selipe/my_home/git/hellonode"
      }
    }

    stage('Build and SonarQube Analysis'){
      steps{
        withSonarQubeEnv('sonar-7.1') {
        sh 'mvn clean package sonar:sonar'
        //sh "mvn clean package"
          }
        }
      }

    stage("Quality Gate") {
         steps {
             timeout(time: 10, unit: 'MINUTES') {
                 // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                 // true = set pipeline to UNSTABLE, false = don't
                 // Requires SonarQube Scanner for Jenkins 2.7+
                 waitForQualityGate abortPipeline: true
             }
         }
     }

    stage('Test'){
      steps{
        archiveArtifacts artifacts: 'Users/selipe/.jenkins/workspace/**/*.jar', fingerprint: true
        junit 'Users/selipe/.jenkins/workspace/**/*.xml'
          }
    }

    stage('Email Notification'){
     steps{
       mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'Hello from Jenkins...!!!', to: 'mrinn777@gmail.com'
         }
    }


    stage('Build Image'){
     steps{
      def app
      app = docker.build("selipe/node")
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
