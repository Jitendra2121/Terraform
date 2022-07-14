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
		sh 'python --version'
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
                sh 'sudo terraform output Terraform_EC2_Public_IP | sudo tee /tmp/replace.txt'
                }
            }
        }
        
        stage("Trigerring Ansible Job") {
            steps {
                build job: 'Ansible'
                echo "Trigerring Ansible Job"
            }
        } 
    }
}
