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
	stage('pre cleanup'){
            steps{
                sh 'rm -rf *'
                sh 'rm -rf .[!.]* ..?*'
            }
        }
        stage('Fetching Source'){
            steps{
                script{
                    git branch: 'main', credentialsId:'GithubAssignment5', url: 'git@github.com:Yorbenxd/calculator-app-finished'
		    sh 'ls -lah'
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
                sh 'mkdir bundle'
                sh 'mv app.js Dockerfile package-lock.json routes.js docker-compose.yml package.json public server.js bundle'
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
