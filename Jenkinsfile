pipeline {
    agent any
    tools {
        nodejs 'TINnode-devops'
    }
    stages {
        stage('opdracht 5') {
            steps {
                echo "good luck..."
            }
        }
        stage('Fetching Source'){
            steps{
                script{
                    // Haal de code uit de git repo binnen
                    git branch: 'main', credentialsId:'', url: 'https://github.com/Yorbenxd/calculator-app-finished'
                }
            }
        }
        stage('install dependencies'){
            steps {
                sh 'npm install'
            }
        }
        stage('Unittest'){
            steps{
                sh 'npm test'
                junit 'junit-report.xml'
            }
        }
    }
}
