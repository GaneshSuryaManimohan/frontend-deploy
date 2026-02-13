pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters {
        string(name: 'APP_VERSION', defaultValue: '1.0.0', description: 'What is the app version?')
    }
    environment{
         APP_VERSION = '' // Variable Declaration
         NEXUS_URL = 'nexus.surya-devops.site:8081'
    }
    stages {
        stage('print the version'){
            steps{
                script{
                    echo "application version: ${params.APP_VERSION}"
                }
            }
        }
        stage('Init Terraform'){
            steps{
                sh """
                    cd terraform
                    terraform init
                """
            }
        }
        stage('Plan Terraform'){
            steps{
                sh """
                    cd terraform
                    terraform plan -var="app_version=${params.APP_VERSION}"
                """
            }
        }
        stage('Apply Terraform'){
            steps{
                sh """
                    cd terraform
                    terraform apply -auto-approve -var="app_version=${params.APP_VERSION}"
                """
            }
        }

    }
    post {
        always {
            echo 'I will always say hello'
            deleteDir()
        }
        success {
            echo 'Shows Only upon success'
        }
        failure {
            echo 'shows upon failure'
        }
    }
}