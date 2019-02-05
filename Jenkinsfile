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
        //           ansiblePlaybook(
          //             playbook: 'exam.yml',
            //           inventory: 'inventory/hosts.yml',
           //            credentialsId: 'ansible-playbook',
          //             sudo: 'true',
                       extras: '--vault-password-file .vault_pass')
                sh 'echo $ANSIBLE_VAULT_CREDS_PSW > .vault_pass'
          //      sh 'cat .vault_pass'
                sh 'id'
                sh 'ansible-playbook -i inventory/hosts.yml exam.yml --vault-password-file .vault_pass'
          //      sh 'sudo ansible-playbook -i inventory/hosts.yml exam.yml --vault-password-file .vault_pass' 
                sh 'rm -f .vault_pass'

        //        withCredentials([file(credentialsId: 'ansible-vault', variable: 'ansibleVaultKeyFile')]) {
        //            ansiblePlaybook(
        //                playbook: 'exam.yml',
        //                inventory: 'inventory/hosts.yml',
        //                credentialsId: 'ansible-playbook',
        //                extras: '--vault-password-file ${ansibleVaultKeyFile}')
        //        }
            }
        }
    }
}
