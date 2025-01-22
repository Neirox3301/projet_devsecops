pipeline {
    agent none
    stages {
        stage("Build & Analyse avec SonarQube") {
            agent any
            steps {
                script {
                    // Commande Maven pour compiler et exécuter l'analyse SonarQube
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
    }
}
