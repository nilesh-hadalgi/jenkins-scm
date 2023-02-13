quay pass : J\;9TK`?^w-.d&3j
usernmae : nilesh_hadalgi

jenkins pass : xp*p7NuB.2PXtR]XN

quay id : 8617fb4f-26f3-4e2a-996c-ca77885b19a3




git add .
git commit -m "."
git push


sudo chown jenkins:jenkins /home/ubuntu/Nilesh/jenkins-files/*
sudo chmod 755 /home/ubuntu/Nilesh/jenkins-files/*


cp /home/ubuntu/Nilesh/jenkins-files/* /var/lib/jenkins/workspace/vm-pipeline/

cp jenkins-files/* /var/lib/jenkins/workspace/vm-pipeline/

sudo chown ubuntu:ubuntu /var/lib/jenkins/workspace/vm-pipeline/



kubectl describe secret -n default $(kubectl get secrets -n default | grep default | awk '{print $1}') | grep token: | awk '{print $2}'

kubectl create secret generic ns-for-token --from-literal=token=$(kubectl get secrets -o jsonpath='{.items[?(@.metadata.annotations["kubernetes\.io/service-account\.name"]=="default")].data.token}' | base64 -d) -n default



kubectl config set-context <context-name> --cluster=<cluster-name> --user=<user-name>


sudo chown -R newuser:newuser /var/lib/jenkins
sudo nano /etc/sysconfig/jenkins


sudo chown -R ubuntu:ubuntu ${ITEM_ROOTDIR}/builds




pipeline {
    agent any

    stages {
        stage('Retrieve YAML file and Apply it') {
            steps {
                script {
                    def yamlFile = ''
                    withCredentials([string(credentialsId: '<credentials-id>', variable: 'yamlFile')]) {
                        // Write the YAML file content to a temporary file
                        def tempFile = "${env.WORKSPACE}/temp.yaml"
                        writeFile file: tempFile, text: yamlFile

                        // Apply the YAML file using kubectl
                        sh "kubectl apply -f ${tempFile}"
                    }
                }
            }
        }
    }
}







---------------------





        stage("delete cache "){
            steps {
                script {
                    withCredentials([[
                        $class: 'FileBinding',
                        credentialsId: 'ec2-pem-file',
                        variable: 'PEM_FILE'
                    ]]) {
                        sshagent(['jenkins-ec2-ssh-key']) {
                            sh "chmod 400 ${PEM_FILE}"
                            // sh "ssh -o StrictHostKeyChecking=no -i ${PEM_FILE} ubuntu@54.174.129.48  kubectl delete secret az-secret -n jenkins-vm" 
                            // sh "ssh -o StrictHostKeyChecking=no -i ${PEM_FILE} ubuntu@54.174.129.48 kubectl delete pod az-pod -n jenkins-vm"
                            // sh "ssh -o StrictHostKeyChecking=no -i ${PEM_FILE} ubuntu@54.174.129.48  kubectl delete namespace jenkins-vm"
                        }
                    }
                }
            }
        }