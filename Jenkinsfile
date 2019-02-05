pipeline {
    agent any

    environment {
        PATH = "/usr/local/bin:/usr/local/sbin:/home/jenkins/.local/bin:$PATH"
        ANSIBLE_VAULT_CREDS = credentials('ansible-vault')
    }

    stages {
        stage('Download roles') {
            steps {   
                sh 'ansible-galaxy install -r requirements.yml'
            }
        }

        stage('Run ansible-playbook') {
            steps {
                sh 'echo $ANSIBLE_VAULT_CREDS_PSW > .vault_pass'
                sh 'ansible-playbook -i inventory/hosts.yml exam.yml --vault-password-file .vault_pass'
                sh 'rm -f .vault_pass'
            }
        }
    }
}
