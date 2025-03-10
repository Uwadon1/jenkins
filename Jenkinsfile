pipeline {
    agent any
   
    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')

    }

    tools {
        terraform 'Terraform'  // Specify the Terraform installation name from the Global Tool Configuration
    }
  
    stages {
        stage('Checkout Code') {
            steps {
                // che
                checkout scm
            }
        }

        stage('Terraform Init') {
            steps {
                // Initialize the Terraform working directory
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                // Generate and display an execution plan
                sh 'terraform plan' 
            }
        }

           stage('Manual Approval') {
            steps {
                script {
                    input message: 'Do you want to proceed with the deployment?', ok: 'Yes, deploy!'
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                // Apply the Terraform plan automatically
                sh 'terraform apply --auto-approve' 
            }
        }

         stage('Terraform Destroy') {
            steps {
                // Destroy the infrastructure automatically
                sh 'terraform destroy --auto-approve'
            }
        }
    }

    post {
        success {
            echo 'Terraform commands executed successfully.'
        }
        failure {
            echo 'Terraform execution failed.'
        }
    }
}

