pipeline {
    agent any

    tools {
        // Use Maven tool configured as "M398" in Jenkins
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
                // Optional Git checkout
                // git 'https://github.com/altamashGit/parameterized-pipeline-job-init.git'
                sh "mvn clean package -DskipTests=true"
            }
        }

        stage('Unit test') {
            steps {
                script {
                    // Countdown loop (60 seconds)
                    for (int i = 0; i < 60; i++) {
                        echo "Countdown: ${i + 1}"
                        sleep 1
                    }

                    // Run tests and build again (inside script block)
                    sh "mvn test"
                    sh "mvn clean package -DskipTests=true"
                }
            }
        }
    }
}