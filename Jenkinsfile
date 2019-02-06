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
                ansiblePlaybook become: true, credentialsId: 'ansible_ssh', disableHostKeyChecking: true, installation: 'ansible', inventory: '/home/jenkins/workspace/Jenkins_CD/inventory/hosts.yml', playbook: '/home/jenkins/workspace/Jenkins_CD/exam.yaml', vaultCredentialsId: 'ansible-vault-key'
            }
        }
    }
}
