pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M398"
    }

    stages {
        stage('Echo Version') {
            steps {
                sh 'echo Print Maven Version'
                sh 'mvn -version'
            }
        }

         stage('Build') {
             steps {
                  // Get some code from a GitHub repository
                // git 'https://github.com/altamashGit/parameterized-pipeline-job-init.git'

                 // Run Maven on a Unix agent.
                 sh "mvn clean package -DskipTests=true"
             }
             
         }
                
                 
         stage('Unit test') {
              steps {
                  sh "mvn test"
                     sh "mvn clean package -DskipTests=true"
              }
         }
    }
}
