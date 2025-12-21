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
                    url: "https://github.com/MATHIVANANIGRIS/jenkinsec2.git"
            }
        }

        stage('Terraform Steps') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credesss'
                ]]) {

                    script {
                        echo "Checking if Terraform is installed..."

                        def terraformCheck = bat(
                            script: 'terraform -version',
                            returnStatus: true
                        )

                        if (terraformCheck != 0) {
                            error "Terraform is not installed or not in PATH!"
                        }

                        echo "Terraform is installed. Running Init, Plan, Apply..."

                        dir('terraform') {
                            bat 'terraform init'
                            bat 'terraform plan'
                            bat 'terraform apply -auto-approve'
                        }

                        echo "Terraform execution completed successfully."
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Jenkins pipeline completed successfully!"
        }
        failure {
            echo "Jenkins pipeline failed!"
        }
    }
}
