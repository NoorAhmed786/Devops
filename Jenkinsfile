pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'git@github.com:NoorAhmed786/devops.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the app for the dev environment...'
                sh 'echo "Build commands for dev"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to Dev server...'
                sh 'scp index.html user@dev-server:/var/www/noor.com/public_html/'
            }
        }
    }
}
