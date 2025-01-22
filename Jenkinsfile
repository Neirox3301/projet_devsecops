pipeline {
    agent any
    tools {
        maven 'Maven_Auto_Install'
    }
    stages {
        stage('Build & Analyse avec SonarQube') {
            steps {
                script {
                    // Commande Maven pour construire et analyser
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
    }
}
