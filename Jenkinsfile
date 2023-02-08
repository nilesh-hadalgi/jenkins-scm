pipeline {
    agent any
    stages {
        stage('Login to Quay') {
         steps {
            script {
            def myCredential = credentials('8617fb4f-26f3-4e2a-996c-ca77885b19a3')
            sh "docker login quay.io -u ${myCredential.username} -p ${myCredential.password}"

         }
      }
        stage('docker-Build') {
            steps {
                script {
                    // Use the Docker plugin to build the image
                    sh "docker build -t awsvmscheduler:v1.0 ."
                    sh "docker tag azurescheduler:v1.0 quay.io/nilesh_hadalgi/awsvmscheduler:v1.0"
                }
            }
        }
        stage('docker-push') {
            steps {
                script {
                    // Use the Docker plugin to build the image
                    sh "docker push quay.io/nilesh_hadalgi/awsvmscheduler:v1.0"
                }
            }
        }
    }
}