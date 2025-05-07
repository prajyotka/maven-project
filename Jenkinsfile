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
  }
}