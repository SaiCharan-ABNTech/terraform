pipeline {
    agent any
    stages {
        stage('Checkout from Git') {
            steps {
                git branch: 'main', url: 'https://github.com/SaiCharan-ABNTech/terraform.git'
            }
        }
        stage('Terraform init') {
            steps {
                dir('terraform') {
                    bat 'terraform init'
                }
            }
        }
        stage('Terraform validate') {
            steps {
                dir('terraform') {
                    bat 'terraform validate'
                }
            }
        }
        stage('Terraform apply') {
            steps {
                dir('terraform') {
                    // Define the action here, whether it's apply or destroy
                    script {
                        def action = 'apply' // or 'destroy'
                        bat "terraform ${action} --auto-approve"
                    }
                }
            }
        }
    }
}
