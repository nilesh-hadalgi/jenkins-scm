pipeline {
    agent any

    stages {
        stage('Login to EC2 Instance') {
            steps {
                 script {
                withCredentials([sshUserPrivateKey(credentialsId: 'ec2-pem', usernameVariable: 'EC2_USER', keyFileVariable: 'EC2_PEM')]) {
                    sh '''
                    echo $EC2_USER
                    #!/bin/bash
                    
                    # Set the hostname or public IP of the EC2 instance
                    HOSTNAME="34.206.28.255"
                    
                    # Connect to the EC2 instance using the PEM file and hostname/IP
                    ssh -i "$EC2_PEM" "$EC2_USER@$HOSTNAME"
                    '''
                }
                }
            }
        }

        stage('Run kubectl Commands') {
            steps {
                 script {
                sh '''
                #!/bin/bash
                
                # Run kubectl commands
                kubectl get pods
                '''
            
            }
            }
        }
    }
}
