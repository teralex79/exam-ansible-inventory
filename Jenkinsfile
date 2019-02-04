pipeline {
    agent any
    stages {
        stage('Download roles') {

            sh 'ansible-galaxy install -r requirements.yml'
        }

        stage('Run ansible-playbook') {
            withCredentials(credentialsId: ansible-vault, passwordVariable: 'PASSWORD') { 
                sh 'echo $PASSWORD > .vault_pass'
                sh 'ansible-playbook -i inventory/hosts.yml exam.yml --vault-password-file .vault_pass'
                sh 'rm -f .vault_pass'
            }
        }
    }
}
