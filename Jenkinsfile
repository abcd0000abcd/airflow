pipeline {
    agent any

    environment {
        AIRFLOW_SERVER = '192.168.0.137'     // Replace with your Airflow server's hostname or IP
        AIRFLOW_USER = 'vishal'                     // Replace with your Airflow server's username
        SOURCE_FILE = '/workspace/*'   // Replace with the path of the file on Jenkins
        DESTINATION_PATH = '/home/vishal' // Replace with destination path on Airflow
    }

    stages {
        stage('Transfer Files to Airflow') {
            steps {
                script {
                    // Optional: Set up an SSH agent if needed
                    //sshagent(['jenkins-ssh-key-id']) { // Replace with Jenkins SSH credentials ID if using SSH agent
                        sh """
                            echo "Transferring files to Airflow server..."
                            scp -o StrictHostKeyChecking=no $SOURCE_FILE ${AIRFLOW_USER}@${AIRFLOW_SERVER}:$DESTINATION_PATH
                            echo "Files successfully transferred."
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Files were successfully moved to the Airflow server."
        }
        failure {
            echo "Failed to transfer files to the Airflow server."
        }
    }
}

