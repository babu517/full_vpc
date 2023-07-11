pipeline {
    agent any
    stages {
     stage('Git Checkout') {
            steps {
                git branch: 'test', credentialsId: 'git', url: 'https://github.com/babu517/full_vpc.git'
            }
        } 
        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
            
        }
        stage('Terraform Plan') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws_credentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
                {
                sh 'terraform plan'
                }
            }
            }
        stage('Terraform Apply') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws_credentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
                {
                sh 'terraform apply --auto-approve'
                }
            }
        }
    
    }
}

