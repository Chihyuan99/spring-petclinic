pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Build petclinic.jar') {
            steps {
                sh 'mvn package'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    sh 'mvn sonar:sonar \
                        -Dsonar.projectKey=petclinic \
                        -Dsonar.host.url=http://18.212.76.116/:9000 \
                        -Dsonar.login=sqa_85926f9b090665e790263e1bcc3e9bacca5dce2e'
                }
            }
        }
    }
}

