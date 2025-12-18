pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = "eu-north-1"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/MATHIVANANIGRIS/jenkinsec2.git', branch: 'main'
            }
        }

        stage('Terraform Init') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credsss'
                ]]) {
                    bat '''
                        cd infra
                        terraform init
                    '''
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credsss'
                ]]) {
                    bat  '''
                        cd infra
                        terraform plan
                    '''
                }
            }
        }

        stage('Terraform Apply') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credsss'
                ]]) {
                    bat  '''
                        cd infra
                        terraform apply -auto-approve
                    '''
                }
            }
        }
    }
}
