pipeline {
    agent any
    options {
        skipDefaultCheckout(true)
    }
    tools
    {
        'org.jenkinsci.plugins.docker.commons.tools.DockerTool' 'Default'
        'terraform' 'Default'
    }
    stages {
        stage('clean workspace') {
            steps {
                cleanWs()
            }
        }
        stage('checkout') {
            steps {
                checkout scm
            }
        }
    stage('tfsec') {
      steps {
        bat ' docker --version'
      }
    }
    stage('Approval for Terraform') {
            steps {
                input(message: 'Approval required before Terraform', ok: 'Proceed', submitterParameter: 'APPROVER')
            }
        }

        stage('terraform') {
            steps {
                bat 'terraform init'
                bat 'terraform apply -auto-approve -no-color'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
