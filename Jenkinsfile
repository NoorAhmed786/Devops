pipeline {
    agent any

    environment {
        DEV_SERVER_IP = '192.168.56.105'            // Replace with your server IP
        USERNAME = 'vboxuser'                       // Replace with your server username
        PRIVATE_KEY_PATH = '/var/lib/jenkins/.ssh/id_ed25519' // Jenkins SSH key path
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out repository from GitHub...'
                git branch: 'main',
                    url: 'git@github.com:NoorAhmed786/Devops.git',
                    credentialsId: 'GitHub SSH Key'  // Replace with your credentials ID
            }
        }

        stage('Build') {
            steps {
                echo 'Build stage (if any build steps are needed)...'
                sh 'echo "Build completed"'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying all changes to ${DEV_SERVER_IP}..."

                sh """
                    rsync -avz --delete --exclude ".git/" \
                    -e "ssh -i ${PRIVATE_KEY_PATH} -o StrictHostKeyChecking=no" \
                    ${WORKSPACE}/ ${USERNAME}@${DEV_SERVER_IP}:/var/www/noor.com/public_html/
                """
            }
        }
    }
}

