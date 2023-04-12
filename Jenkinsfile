pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
        steps {
            def mvn = tool 'Default Maven';
            sh "${mvn}/bin/mvn clean install"
        }
    }
    stage('SonarQube analysis') {
      steps {
        def mvn = tool 'Default Maven';
        withSonarQubeEnv() {
          sh "${mvn}/bin/mvn clean verify sonar:sonar \
              -Dsonar.projectKey=petclinic \
              -Dsonar.host.url=http://3.16.49.56:9000 \
              -Dsonar.login=sqp_bee15a8a76900d3bbfaf1e698b5c0867bc5a5803"
        }
      }
    }
    stage('Build petclinic.jar') {
      steps {
        def mvn = tool 'Default Maven';
        sh "${mvn}/bin/mvn package"
        sh "cp target/*.jar petclinic.jar"
      }
    }
  }
}

