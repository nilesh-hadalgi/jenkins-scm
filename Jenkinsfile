pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Use the Docker plugin to build the image
                    sh "docker build -t awsvmscheduler:v1.0 ."
                    sh "docker tag azurescheduler:v1.0 quay.io/manoj_dhanorkar/awsvmscheduler:v1.0"
                    sh "docker push quay.io/manoj_dhanorkar/awsvmscheduler:v1.0"
                }
            }
        }
    }
}
