pipeline {
    agent any

    environment {
        PATH = "/usr/local/bin:/usr/local/sbin:/home/jenkins/.local/bin:$PATH"
        ANSIBLE_VAULT_CREDS = credentials('ansible-vault')
     //   ANSIBLE_SSH_CREDS = credentials('ansible-playbook')
    }

    stages {
        stage('Download roles') {
            steps {   
                sh 'ansible-galaxy install -r requirements.yml'
            }
        }

        stage('Run ansible-playbook') {
            steps {
                ansiblePlaybook( colorized: true, credentialsId: 'ansible-playbook', disableHostKeyChecking: true, installation: 'ansible', inventory: 'inventory/hosts.yml', playbook: 'exam.yaml', vaultCredentialsId: 'ansible-vault-plugin')
            }
        }
    }
}
