pipeline {
  agent any
    stages {
      stage('Maven Build') {
        steps {
        sh 'mvn clean package'
        }
      }
    stage('Deploy to Tomcat') {
      steps {
        echo "coning soon..."
      }
    }
  }
  post {
    success {
      archiveArtifacts artifacts: 'target/*.war'
      cleanWs()
    }
  }
}
