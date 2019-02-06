pipeline {
    agent any

    environment {
        PATH = "/usr/local/bin:/usr/local/sbin:/home/jenkins/.local/bin:$PATH"
    }

    stages {
        stage('Download roles') {
            steps {   
                sh 'ansible-galaxy install -r requirements.yml'
            }
        }

        stage('Run ansible-playbook') {
            steps {
                ansiblePlaybook( become: true,
                                 credentialsId: 'ansible_ssh', 
                                 disableHostKeyChecking: true, 
                                 installation: 'ansible',
                                 inventory: 'inventory/hosts.yml', 
                                 playbook: 'exam.yaml', 
                                 vaultCredentialsId: 'ansible-vault-key')

            }
        }
    }
}
