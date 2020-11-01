pipeline {
   agent any

   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "M3"
   }

   stages {
//      stage('git'){
//           steps {
//            // Get some code from a GitHub repository
//            //git 'https://github.com/jarviscanada/jarvis_cicd_demo_app.git'
//            git branch: 'develop', url: 'https://github.com/jarviscanada/jarvis_cicd_demo_app.git'
//            }
//      }
      stage('Maven build') {
         steps {
            // Run Maven on a Unix agent.
            sh "mvn clean clean package"
         }

         post {
            // archive the jar file.
            success {
               archiveArtifacts 'target/*.jar'
            }
         }
      }
      stage('Docker build') {
         steps {
            // Run Maven on a Unix agent.
            sh "docker build -t jrvs/simple_app ."
            sh "docker push jrvs/simple_app"
         }
      }

      stage('Deoply dev') {
         steps {
            sh "ssh service@app-server-dev docker pull jrvs/simple_app ; docker stop simple_app; docker run ...."
         }
      }
   }
}
