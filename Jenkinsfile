pipeline {
    agent any
    stages {
        stage('docker-Build') {
            steps {
                 script {
                    sh "cp /home/ubuntu/Nilesh/jenkins-files/Dockerfile $WORKSPACE"
                    sh "cp /home/ubuntu/Nilesh/jenkins-files/AWSVMScheduler $WORKSPACE"
                    
                    sh "docker build -t awsvmscheduler:v1.0 ."
                    sh "docker tag azurescheduler:v1.0 quay.io/nilesh_hadalgi/awsvmscheduler:v1.0"
                }
            }
        }
        stage('docker-push') {
            steps {
                script {
                     withCredentials([usernamePassword(credentialsId: '8617fb4f-26f3-4e2a-996c-ca77885b19a3', usernameVariable: 'QUAY_USERNAME', passwordVariable: 'QUAY_PASSWORD')]) {
                    sh 'docker login quay.io -u $QUAY_USERNAME -p $QUAY_PASSWORD'
                }// Use the Docker plugin to build the image
                    sh "docker push quay.io/nilesh_hadalgi/awsvmscheduler:v1.0"
                }
            }
        }
          stage('create-and-pod') {
            steps {
                script {
                    sh "kubectl create -f aws-secret.yaml -n jenkins-vm"
                    sh "kubectl create -f aws-pod.yaml -n jenkins-vm"
                }
            }
        }
    } 
}