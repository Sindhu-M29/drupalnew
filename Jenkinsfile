pipeline {
    agent any
    
    environment {
        INSTANCE_IP = '107.21.87.127' // Update with your instance2 IP address
    }
    
    stages {
        stage('Checkout') {
            steps {
                git(
                    credentialsId: '70164c8d-fcb0-473b-8c1a-d8d601a4ddc6',
                    branch: 'main',
                    url: 'https://github.com/Sindhu-M29/drupalnew.git'
                )
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    // Use credentials for SSH authentication
                    withCredentials([usernamePassword(credentialsId: '66ecbb51-faa1-44e5-858b-bf2efd064f2c', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                        sh '''
                        # Define the source and destination directories
                        SRC_DIR=$(pwd)
                        DEST_DIR=/var/www/html
                        
                        # Use rsync to copy only the changed files to the target instance
                        rsync -avz --delete -e "sshpass -p $PASS ssh -o StrictHostKeyChecking=no" $SRC_DIR/ $USER@$INSTANCE_IP:$DEST_DIR/
                        '''
                    }
                }
            }
        }
    }
}
