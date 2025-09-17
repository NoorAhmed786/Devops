pipeline {
    agent any

    environment {
        DEV_SERVER_IP = '192.168.56.105'  // Replace with your actual IP address
        USERNAME = 'vboxuser'             // Replace with your actual username
        PRIVATE_KEY_PATH = '/var/lib/jenkins/.ssh/id_ed25519'  // Path to the private key
    }

    stages {
        stage('Check SSH Key') {
            steps {
                script {
                    // Check if the private key exists
                    if (fileExists("${PRIVATE_KEY_PATH}")) {
                        echo "Private key exists, proceeding with deployment..."
                    } else {
                        error "Private key does not exist at ${PRIVATE_KEY_PATH}, cannot proceed with deployment."
                    }
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building the app...'
                sh 'echo "Build commands for dev"'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${DEV_SERVER_IP}..."

                // Check if the file exists before running rsync
                sh 'ls -l index.html'  // This will list the file if it exists

                // Rsync deployment command
                sh """
                    rsync -avz -e 'ssh -i ${PRIVATE_KEY_PATH} -o StrictHostKeyChecking=no' index.html ${USERNAME}@${DEV_SERVER_IP}:/var/www/noor.com/public_html/
                """
            }
        }
    }
}
