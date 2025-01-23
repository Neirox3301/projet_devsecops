pipeline {
    agent any
    tools {
        maven ''Maven_Auto_Install'
    }
    
    stages {
        stage('Building Application') {
            steps {
                echo 'Building Application'
                sh 'mvn compile'
            }
        }
        
        stage('Sonarqube analysis') {
            environment {
                SONAR_HOST_URL = 'http://192.168.56.1:9000/'
                SONAR_AUTH_TOKEN = credentials('TokenSonarQube3')
            }
            steps {
                echo 'Sonarqube analysis'
                sh '''
                mvn sonar:sonar \
                    -Dsonar.projectKey=sample_project \
                    -Dsonar.host.url=$SONAR_HOST_URL \
                    -Dsonar.login=$SONAR_AUTH_TOKEN
                '''
            }
        }
    }
}
