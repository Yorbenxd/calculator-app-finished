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
        stage('Create bundle'){
            steps {
                sh 'mkdir -p bundle'
                sh 'cp -r .dockerignore .gitignore Dockerfile Jenkinsfile docker-compose.yml package.json README.md tests'
                sh 'zip -r bundle.zip bundle'
            }
        }
    }
    post {
        failure {
            script{
                def date = new Date().format("yyyy-MM-dd HH:mm")
                sh "echo 'pipeline poging faalt op ${date}' >> /var/lib/jenkins/logs/jenkinserrorlog"
            }
        }
        success{
            archiveArtifacts artifacts: 'bundle.zip', fingerprint: true
        }
    }
    triggers {
        cron('H 14 * * 5')
    }
}
