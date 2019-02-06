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
                script {
                    ansiblePlaybook become: true, credentialsId: 'ansible_ssh', disableHostKeyChecking: true, installation: 'ansible', nventory: '/home/jenkins/workspace/Jenkins_CD/inventory/hosts.yml', playbook: '/home/jenkins/workspace/Jenkins_CD/exam.yaml', vaultCredentialsId: 'ansible-vault-key'
                }
            }
        }
    }
}
