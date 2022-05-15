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
        sshagent(['tomcat-dev3']) {
            sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.20.68:/opt/tomcat8/webapps/app.war'
                sh "ssh ec2-user@172.31.20.68 /opt/tomcat8/bin/shutdown.sh"
                sh "ssh ec2-user@172.31.20.68 /opt/tomcat8/bin/startup.sh"
        }
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
