pipeline {
    agent any

    parameters {
        booleanParam(name: 'autoApprove', defaultValue: false, description: 'Automatically run apply after generating plan?')
    } 
    
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

    stages {
        stage('Checkout from Git') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/SaiCharan-ABNTech/terraform.git'
                }
            }
        }

        stage('Plan') {
            steps {
                script {
                    sh 'pwd; cd terraform/ ; terraform init'
                    sh 'pwd; cd terraform/ ; terraform plan -out tfplan'
                    sh 'pwd; cd terraform/ ; terraform show -no-color tfplan > tfplan.txt'
                }
            }
        }

        stage('Approval') {
            when {
                expression {
                    return params.autoApprove == false
                }
            }

            steps {
                script {
                    def plan = readFile 'terraform/tfplan.txt'
                    input message: 'Do you want to apply the plan?',
                          parameters: [text(name: 'Plan', description: 'Please review the plan', defaultValue: plan)]
                }
            }
        }

        stage('Apply') {
            when {
                expression {
                    return params.autoApprove == true
                }
            }

            steps {
                script {
                    sh 'pwd; cd terraform/ ; terraform apply -input=false tfplan'
                }
            }
        }
    }
}
