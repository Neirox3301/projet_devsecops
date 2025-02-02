pipeline {
    agent any
    tools {
        maven 'Maven_Auto_Install'
    }
    
    environment {
        DEPENDENCY_CHECK_HOME = tool name: 'DependencyCheck_Auto', type: 'hudson.plugins.dependencycheck.DependencyCheckInstallation'
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

        stage('deploy & OWASP Dependency-Check') {
            agent any
            steps {
                dependencyCheck additionalArguments: '''
                -o './' \
                -s './' \
                -f 'ALL' \
                --prettyPrint''', 
                odcInstallation: 'owasp-dependency'
                
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }

        stage('Publish Dependency-Check Report') {
            steps {
                echo 'Publishing Dependency-Check Report'
                publishHTML(target: [
                    reportDir: '.',
                    reportFiles: 'dependency-check-report.html',
                    reportName: 'Dependency-Check Report'
                ])
            }
        }
    }
}
