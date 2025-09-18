pipeline {
    agent any

    environment {
        DEV_SERVER_IP = '192.168.56.105'  // Replace with your actual IP address
        USERNAME = 'vboxuser'             // Replace with your actual username
        PRIVATE_KEY_PATH = '/var/lib/jenkins/.ssh/id_ed25519'  // Path to the private key
    }

    stages {

        stage('Deploy') {
            steps {
                echo "Deploying to ${DEV_SERVER_IP}..."

                // Rsync deployment command
                sh """
                    rsync -av --exclude ".git/" \ ${WORKSPACE}/* ${USERNAME}@${DEV_SERVER_IP}:/var/www/noor.com/public_html/
                """
            }
        }
    }
}
