pipeline {
    agent any

    stages {
        stage('Login to EC2 Instance') {
            steps {
                 script {
                withCredentials([sshUserPrivateKey(credentialsId: 'ec2-pem', usernameVariable: 'EC2_USER', keyFileVariable: 'EC2_PEM')]) {
                    sh 'ssh -i "$EC2_PEM" "ubuntu@$34.206.28.255"'
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
