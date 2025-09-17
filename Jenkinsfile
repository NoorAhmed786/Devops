pipeline {
    agent any

    environment {
        // Define the IP and username as environment variables
        DEV_SERVER_IP = '192.168.56.105'  // Replace with your actual IP address
        USERNAME = 'vboxuser'         // Replace with your actual username
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
                    # Copy the index.html to your Dev server using scp
                    scp -o StrictHostKeyChecking=no -i /path/to/your/private_key index.html ${USERNAME}@${DEV_SERVER_IP}:/var/www/noor.com/public_html/
                '''
            }
        }
    }
}

