pipeline {
    agent any
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
    }
}
