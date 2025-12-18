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

        stage('terraform Init') {
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

        stage('terraform Plan') {
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

        stage('terraform Apply') {
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
