pipeline {
    agent any
    environment {
       BUILD_NUMBER_X = "${env.BUILD_NUMBER}"
       TERRAFORM_HOME = "/usr/bin/terraform"
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
                sh 'sudo ${TERRAFORM_HOME} init -upgrade'
                sh 'sudo ${TERRAFORM_HOME} plan' 
                sh 'sudo ${TERRAFORM_HOME} apply --auto-approve'
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
