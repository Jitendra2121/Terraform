pipeline {
    agent any
    environment {
       BUILD_NUMBER_X = "${env.BUILD_NUMBER}"
    }
    stages {
        stage('Test') {
            steps {
                sh 'ansible --version'
            }
        }
        stage('Docker Build') {
            steps {
                echo "${env.BUILD_NUMBER}"
                sh 'cd /home/ubuntu/terraform/vpc'
                sh 'sudo terraform init -upgrade'
                /* sh 'sudo terraform plan' */
                sh 'sudo terraform apply --auto-approve'
                echo 'Build Number: ' + env.BUILD_NUMBER_X
                echo "Succefully push the ${BUILD_NUMBER_X}th version for Terraform"
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
