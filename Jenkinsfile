
   pipeline {
    agent any
 
    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sahdevmandal123/Terraform-Jenkins.git']]])
            }
        }
        stage('init') {
            steps {
                sh ('terraform init') 
            }
        }

       stage('plan') {
            steps {
                sh ('terraform plan') 
            }
        }

      stage('apply') {
            steps {
                sh ('terraform apply') 
            }
        }
        stage('terraform  action') {
            steps {
                echo "Terraform action is --> ${action}"
                sh ('terraform ${action} --auto-approve')
            }
        }
    }
