pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = "us-east-2"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Checking out code from GitHub..."
                git branch: 'main',
                    url: 'https://github.com/MATHIVANANIGRIS/jenkinsec2.git'
            }
        }

        stage('Terraform Steps') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credsss'
                ]]) {

                    script {
                        echo "Checking if Terraform is installed..."

                        def terraformCheck = bat(
                            script: 'C:\\terraform\\terraform.exe -version',
                            returnStatus: true
                        )

                        if (terraformCheck != 0) {
                            error "Terraform is not installed at C:\\terraform\\terraform.exe"
                        }

                        echo "Terraform is installed. Running Init, Plan, Apply..."

                        dir('terraform') {
                            bat 'C:\\terraform\\terraform.exe init'
                            bat 'C:\\terraform\\terraform.exe plan'
                            bat 'C:\\terraform\\terraform.exe apply -auto-approve'
                        }

                        echo "Terraform execution completed successfully."
                    }
                }
            }
        }
    }
}
