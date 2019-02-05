pipeline {
    agent any

    environment {
        PATH="/usr/local/bin:/usr/local/sbin:/home/jenkins/.local/bin:$PATH"
    }

    stages {
        stage('Download roles') {
            steps {   
                sh 'ansible-galaxy install -r requirements.yml'
            }
        }

        stage('Run ansible-playbook') {
            steps {
                withCredentials([usernamePassword(credentialsId: ansible-vault, passwordVariable: 'PASSWORD')]) { 
                    sh 'echo $PASSWORD > .vault_pass'
                    sh 'ansible-playbook -i inventory/hosts.yml exam.yml --vault-password-file .vault_pass'
                    sh 'rm -f .vault_pass'
                }
            }
        }
    }
}
