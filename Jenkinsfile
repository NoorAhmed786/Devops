pipeline {
    agent any
    
    environment {
        DEV_SERVER_IP = '192.168.56.105'
        USERNAME = 'vboxuser'
        PRIVATE_KEY_PATH = '/var/lib/jenkins/.ssh/id_ed25519' // Correct path to your private key
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the app for the dev environment...'
                sh 'echo "Build commands for dev"'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to Dev server at ${DEV_SERVER_IP}..."
                sh '''
                    scp -o StrictHostKeyChecking=no -i ${PRIVATE_KEY_PATH} index.html ${USERNAME}@${DEV_SERVER_IP}:/var/www/noor.com/public_html/
                '''
            }
        }
    }
}
