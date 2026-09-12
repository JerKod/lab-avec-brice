pipeline {
    agent any

    stages {
        // Say Hello
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/JerKod/lab-avec-brice.git'
            }
        }
        
        // Say Hello
        stage('Deploy app') {
            agent {
                docker { 
                    image 'alpine/ansible:2.21.0'
                    reuseNode true
                    args '--privileged --user root'
                }
            }
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'WORKER_SSH_KEY_ID', keyFileVariable: 'SSH_KEY', usernameVariable: 'SSH_USER')]) {
                    ansiColor('xterm') {
                        sh '''
                            ansible-playbook deploy_click_counter.yml -u ${SSH_USER} --private-key ${SSH_KEY}
                        '''
                    }
                }
            }
        }
        
        // test application
        stage('Validation') {
            steps {
                sh '''
                    sleep 10
                    curl -kv http://localhost:8085/
                '''
            }
        }
    }
}
