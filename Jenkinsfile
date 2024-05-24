pipeline{
    agent any
    stages {
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/SaiCharan-ABNTech/terraform.git'
            }
        }
        stage('Terraform init'){
             steps{
                 dir('terraform') {
                      sh 'terraform init'
                   }
             }
        }
        stage('Terraform validate'){
             steps{
                 dir('terraform') {
                      sh 'terraform validate'
                   }
             }
        }
        stage('Terraform plan'){
             steps{
                 dir('terraform') {
                      sh 'terraform plan'
                   }
             }
        }
        stage('Terraform apply/destroy'){
             steps{
                 dir('terraform') {
                      sh 'terraform ${action} --auto-approve'
                   }
             }
        }
    }
}
