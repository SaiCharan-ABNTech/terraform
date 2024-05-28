pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

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
                    bat 'terraform apply'
                }
            }
        }
    }
}
