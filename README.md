pipeline {
    agent any
    
    environment {
        EC2_INSTANCE_DNS = 'your_ec2_instance_dns'
        REPO_URL = 'your_git_repo_url'
        KARATE_TEST_PATH = 'path/to/karate/test.feature'
    }

    stages {
        stage('Connect to EC2') {
            steps {
                script {
                    // Connect to EC2 instance using DNS
                    sshCommand(
                        host: EC2_INSTANCE_DNS,
                        user: 'your_ssh_user',
                        credentialsId: 'your_ssh_credentials_id',
                        command: 'echo Connected to EC2'
                    )
                }
            }
        }

        stage('Clone Repository') {
            steps {
                script {
                    // Clone Git repository
                    git branch: 'main', url: REPO_URL
                }
            }
        }

        stage('Run Commands') {
            steps {
                script {
                    // Run ls command
                    sh 'ls -la'

                    // Run df command
                    sh 'df -h'
                }
            }
        }

        stage('Run Karate Tests') {
            steps {
                script {
                    // Execute Karate framework script
                    sh "karate ${KARATE_TEST_PATH}"
                }
            }
        }
    }
}
