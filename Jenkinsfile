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
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins_slave_rsa',
                                                   keyFileVariable: 'SSH_KEY',
                                                   usernameVariable: 'USER'),
                                 file(credentialsId: 'ansible-vault-key',
                                      variable: 'VAULT_KEY_FILE')]) {
                    sh 'ansible-playbook exam.yml -i inventory/hosts.yml  -e 'host_key_checking=False' --vault-password-file ${VAULT_KEY_FILE} --private-key ${SSH_KEY}'
                }
            }
        }
    }
}
