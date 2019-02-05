pipeline {
    agent any

    environment {
        PATH = "/usr/local/bin:/usr/local/sbin:/home/jenkins/.local/bin:$PATH"
        ANSIBLE_VAULT_CREDS = credentialsId('ansible-vault-plugin')     
        ANSIBLE_SSH_CREDS = credentialsId('ansible-playbook')
    }

    stages {
        stage('Download roles') {
            steps {   
                sh 'ansible-galaxy install -r requirements.yml'
            }
        }

        stage('Run ansible-playbook') {
            steps {
//                ansiblePlaybook( credentialsId: 'ansible-playbook', 
//                                 disableHostKeyChecking: true, 
//                                 inventory: 'inventory/hosts.yml', 
//                                 playbook: 'exam.yaml', 
//                                 vaultCredentialsId: 'ansible-vault-plugin')
               sh 'ansible-playbook exam.yml -i inventory/hosts.yml --vault-password-file $ANSIBLE_VAULT_CREDS --private-key ANSIBLE_SSH_CREDS'   
            }
        }
    }
}
