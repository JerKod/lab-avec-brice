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
            steps {
                sh '''
                    ansible-playbook deploy_click_counter.yml
                '''
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
