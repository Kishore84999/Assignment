pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker-compose build'
            }
        }
        stage('Test') {
            steps {
                sh 'docker-compose run web python manage.py test'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['my-ssh-credentials']) {
                    sh 'scp docker-compose.yml azureuser@<VM_IP>:/home/azureuser/app/'
                    sh 'ssh azureuser@<VM_IP> "cd /home/azureuser/app && docker-compose up -d"'
                }
            }
        }
    }
}
