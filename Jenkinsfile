pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }

    stages {

        stage('GIT') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Inees12/devops_pipe.git',
                    credentialsId: 'jenkins-token' // Ton ID GitHub PAT
            }
        }

        stage('MVN CLEAN') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('MVN COMPILE') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('MVN PACKAGE') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
        stage('Test Sonar Env') {
            steps {
                withSonarQubeEnv('Sonarqube') {
                    sh 'echo "SONAR_HOST_URL=$SONAR_HOST_URL"'
                }
            }
        }

        stage('MVN SONARQUBE') {
            steps {
                withSonarQubeEnv('Sonarqube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        

    }

    post {
        success {
            echo 'Pipeline terminé avec succès !'
        }
        failure {
            echo 'Pipeline échoué.'
        }
    }
}
