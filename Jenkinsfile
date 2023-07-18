pipeline {
    agent any
    
    environment {
        AWS_REGION = 'ap-south-1'  // Update with your desired region
        TERRAFORM_BINARY = '/usr/local/bin/terraform'  // Path to Terraform binary on Jenkins agent
        TERRAFORM_WORKSPACE = 'my-terraform-workspace'  // Name of the Terraform workspace (optional)
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/sahdevmandal123/Terraform-Jenkins.git'
            }
        }
        
        stage('Terraform Init') {
            steps {
                sh "${TERRAFORM_BINARY} init"
            }
        }
        
        stage('Terraform Apply') {
            steps {
                sh "${TERRAFORM_BINARY} apply -auto-approve"
            }
        }
        
        stage('Deploy to EC2') {
            steps {
                sh "ssh -o StrictHostKeyChecking=no ec2-user@${aws_instance.example.public_ip} 'sudo systemctl stop your-app'"  // Stop the application (assuming systemd)
                sh "ssh -o StrictHostKeyChecking=no ec2-user@${aws_instance.example.public_ip} 'sudo rm -rf /path/to/old/your-app.jar'"  // Remove old app (optional)
                sh "ssh -o StrictHostKeyChecking=no ec2-user@${aws_instance.example.public_ip} 'sudo aws s3 cp s3://${AWS_S3_BUCKET}/your-app-${APP_VERSION}.jar /path/to/your-app.jar'"
                sh "ssh -o StrictHostKeyChecking=no ec2-user@${aws_instance.example.public_ip} 'sudo systemctl start your-app'"  // Start the application (assuming systemd)
            }
        }
    }
 }
   
