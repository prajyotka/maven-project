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
    stage('create docker image') //this stage will create docker image
    {
      steps {
            sh 'docker build -t prajyotka/prajyotka:latest .'
          }
        }
    stage('push docker image') //this stage will push image to docker hub
    {
      steps {
        withDockerRegistry(credentialsId: 'dockerHub', url: 'https://index.docker.io/v1/') {
        sh 'docker push prajyotka/prajyotka:latest'
          }
      }
    }
  }
}