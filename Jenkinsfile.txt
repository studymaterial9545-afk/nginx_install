pipeline {
    agent { label 'ansible' }  // run on node with Ansible installed

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/studymaterial9545-afk/nginx_install.git',
                    credentialsId: 'jenkinsAnsible'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                ansible-playbook -i inventory install.yml
                '''
            }
        }
    }

}


