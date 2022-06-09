pipeline {
    agent any
    environment {
       BUILD_NUMBER_X = "${env.BUILD_NUMBER}"
       TERRAFORM_HOME = "/usr/bin/terraform"
    }
    stages {
        stage('Terraform Version') {
            steps {
                sh '${TERRAFORM_HOME} --version'
            }
        }
        stage('Terraform') {
            steps {
                script{
                echo "${env.BUILD_NUMBER}"
                sh 'sudo cp /home/ubuntu/terraform/vpc/terraform/* ./'
                sh 'sudo ${TERRAFORM_HOME} init -upgrade'
                sh 'sudo ${TERRAFORM_HOME} plan'
                sh 'sudo ${TERRAFORM_HOME} apply --auto-approve'
#                EC2_IP = sh 'sudo terraform output Terraform_EC2_Public_IP'
#                echo 'EC2 IP: ' + ${EC2_IP}
#                echo "Succefully created EC2 Instance: ${EC2_IP} for Terraform."
                }
            }
        }
        /* stage("Build_Number_Passing") {
            steps {
                build job: 'eks-gitops-final', parameters: [string(name: 'BUILD_NUMBER_X', value: "${env.BUILD_NUMBER}")]
                echo "Passing the Build Number: ${BUILD_NUMBER_X} to the eks-gitops job"
            }
        } */
    }
}
