pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('Dockerhub')
    }

    stages {
        stage('Docker Login') {
            steps {
                // Correct command for Docker login
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        
        stage('Build & Push Dockerfile') {
            steps {
                // Command to build Docker image and push to DockerHub
                sh '''
                    docker build -t $DOCKERHUB_CREDENTIALS_USR/my-image .
                    docker push $DOCKERHUB_CREDENTIALS_USR/my-image
                '''
            }
        }
        
        stage('Run Ansible Playbook') {
            steps {
                // Execute Ansible playbook
                sh 'ansible-playbook ansible-playbook.yml'
            }
        }
    }
}
