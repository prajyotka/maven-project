pipeline {
  agent any
  stages {
    stage('scm checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/prajyotka/maven-project.git'
      }
    }
    stage('compile job') //valiadte, compile, test & then package
    {
      steps {
          withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
          sh 'mvn clean package'
          }
        }
      }
    stage('Deploy Code') //deploy code on web server
    {
      steps {
          sshagent(['DEV_CICD']) {
            sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.0.16:/usr/share/tomcat/webapps'
          }
        }
      }
  }
}