pipeline {
    agent any

    stages {
        stage("SSH connection "){
            steps {
                script {
                    withCredentials([[
                        $class: 'FileBinding',
                        credentialsId: 'ec2-pem-file',
                        variable: 'PEM_FILE'
                    ]]) {
                        sshagent(['jenkins-ec2-ssh-key']){
                            sh "chmod 400 ${PEM_FILE}"
                            sh "ssh -o StrictHostKeyChecking=no -i ${PEM_FILE} ubuntu@54.174.129.48 echo 'Connection Successful'"
                        }
                    }
                }
            }
        }
        stage("Docker Build and Tag"){
            steps {
                script {
                    withCredentials([[
                        $class: 'FileBinding',
                        credentialsId: 'ec2-pem-file',
                        variable: 'PEM_FILE'
                    ]]) {
                        sshagent(['jenkins-ec2-ssh-key']) {
                            sh "chmod 400 ${PEM_FILE}"
                            sh "ssh -o StrictHostKeyChecking=no -i ${PEM_FILE} ubuntu@54.174.129.48 docker build -f ./Nilesh/jenkins-files/Dockerfile-minimal -t azurevmscheduler:v1.0 ."
                            sh "ssh -o StrictHostKeyChecking=no -i ${PEM_FILE} ubuntu@54.174.129.48 docker tag docker.io/library/azurevmscheduler:v1.0 quay.io/manoj_dhanorkar/azurevmscheduler:v1.0"
                        }
                    }
                }
            }
        }
         stage("Docker Push"){
            steps {
                script {
                    withCredentials([[
                        $class: 'FileBinding',
                        credentialsId: 'ec2-pem-file',
                        variable: 'PEM_FILE'
                    ]]) {
                        sshagent(['jenkins-ec2-ssh-key']) {
                            sh "chmod 400 ${PEM_FILE}"
                            sh "ssh -o StrictHostKeyChecking=no -i ${PEM_FILE} ubuntu@54.174.129.48 docker push quay.io/manoj_dhanorkar/azurevmscheduler:v1.0"
                        }
                    }
                }
            }
        }
         stage("Create Name Space"){
            steps {
                script {
                    withCredentials([[
                        $class: 'FileBinding',
                        credentialsId: 'ec2-pem-file',
                        variable: 'PEM_FILE'
                    ]]) {
                        sshagent(['jenkins-ec2-ssh-key']) {
                            sh "chmod 400 ${PEM_FILE}"
                            sh "ssh -o StrictHostKeyChecking=no -i ${PEM_FILE} ubuntu@54.174.129.48  kubectl create namespace jenkins-vm || echo 'namespace already exists'"
                        }
                    }
                }
            }
        }
        stage("Apply Secrets"){
            steps {
                script {
                    withCredentials([[
                        $class: 'FileBinding',
                        credentialsId: 'ec2-pem-file',
                        variable: 'PEM_FILE'
                    ]]) {
                        sshagent(['jenkins-ec2-ssh-key']) {
                            sh "chmod 400 ${PEM_FILE}"
                            sh "ssh -o StrictHostKeyChecking=no -i ${PEM_FILE} ubuntu@54.174.129.48  kubectl apply -f ./Nilesh/jenkins-files/az-secret.yaml -n jenkins-vm"
                        }
                    }
                }
            }
        }
        stage("Apply Pod Spec"){
            steps {
                script {
                    withCredentials([[
                        $class: 'FileBinding',
                        credentialsId: 'ec2-pem-file',
                        variable: 'PEM_FILE'
                    ]]) {
                        sshagent(['jenkins-ec2-ssh-key']) {
                            sh "chmod 400 ${PEM_FILE}"
                            sh "ssh -o StrictHostKeyChecking=no -i ${PEM_FILE} ubuntu@54.174.129.48  kubectl apply -f ./Nilesh/jenkins-files/az-pod.yaml -n jenkins-vm"
                        }
                    }
                }
            }
        }





    }
}
