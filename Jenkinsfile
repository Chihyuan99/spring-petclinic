node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'Default Maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=Petclinic -Dsonar.projectName='Petclinic'"
    }
  }
  stage('Build JAR') {
    def mvn = tool 'Default Maven';
    sh "${mvn}/bin/mvn package"
    sh "cp target/*.jar petclinic.jar"
  }
  stage('Run JAR') {
    sh "java -jar -Dserver.port=8081 petclinic.jar"
  }
}
