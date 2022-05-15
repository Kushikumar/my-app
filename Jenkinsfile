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
          sshagent(['tomcat-deb']) {
              //copy war file to tomcat server
              sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.3.73:/opt/tomcat8/webapps/app.war'
              //stop tomcat
              sh "ssh ec2-user@172.31.3.73 /opt/tomcat8/bin/shutdown.sh"
              //start tomcat
              sh "ssh ec2-user@172.31.3.73 /opt/tomcat8/bin/startup.sh"
              
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
