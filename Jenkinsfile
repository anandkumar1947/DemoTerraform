pipeline {
    agent any

    environment {
        TF_AUTO_APPROVE = 'true' // Set to 'true' for auto-approval
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/anandkumar1947/DemoTerraform.git'
            }
        }
        stage('Terraform Actions') {
            when {
                expression { return "${params.RUN_DEPLOYMENT}" == 'true' }
            }
            steps {
                sh 'terraform init'
                sh 'terraform plan'
                sh 'terraform apply -auto-approve'
            }
        }
        stage('Terraform Destroy') {
            when {
                expression { return "${params.RUN_DEPLOYMENT}" != 'true' }
            }
            steps {
                sh 'terraform destroy -auto-approve'
            }
        }
    }

    parameters {
        booleanParam(name: 'RUN_DEPLOYMENT', defaultValue: false, description: 'Run Terraform Deployment?')
    }
}
