pipeline {
  agent any

  parameters {
    string(name: 'SLEEP_TIME', defaultValue: '5', description: 'Time to wait before integration testing')
    string(name: 'APP_PORT', defaultValue: '8080', description: 'Port where app runs')
    string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'Branch name to build')
  }

  tools {
    maven 'M398'
  }

  stages {
    stage('Maven Version') {
      steps {
        sh 'echo Print Maven Version'
        sh 'mvn -version'
        sh "echo Sleep-Time - ${params.SLEEP_TIME}, Port - ${params.APP_PORT}, Branch - ${params.BRANCH_NAME}"
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests=true'
        archiveArtifacts 'target/hello-demo-*.jar'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
        junit(testResults: 'target/surefire-reports/TEST-*.xml', keepProperties: true, keepTestNames: true)
      }
    }

    stage('Local Deployment') {
      steps {
        sh 'nohup java -jar target/hello-demo-*.jar > /dev/null 2>&1 &'
      }
    }

    stage('Integration Testing') {
      steps {
        sh "sleep ${params.SLEEP_TIME}"
        sh "curl -s http://localhost:${params.APP_PORT}/hello"
      }
    }
  }
}
