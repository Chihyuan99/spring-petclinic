pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        sshagent(['ssh_rsa']) {
          git credentialsId: 'ssh_rsa', branch: 'main', url: 'git@github.com:Chihyuan99/spring-petclinic.git'
        }
      }
    }
    stage('Build') {
        steps {
            sh 'mvn clean install'
        }
    }
    stage('SonarQube analysis') {
      steps {
        withSonarQubeEnv('SonarQube') {
          sh 'mvn clean verify sonar:sonar \
              -Dsonar.projectKey=petclinic \
              -Dsonar.host.url=http://54.159.13.113:9000 \
              -Dsonar.login=sqa_2145f8990d1f08f072bec12bf068b21a5296f56c'
        }
      }
    }
    stage('Build petclinic.jar') {
      steps {
        sh 'mvn package'
      }
    }
  }
}
