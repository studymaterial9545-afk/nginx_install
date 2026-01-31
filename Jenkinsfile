pipeline {
    agent {
        label 'tomcat'
    }

    environment {
        ANSIBLE_PLAYBOOK = "deploy.yml"
        INVENTORY_FILE   = "inventory"
    }

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
                    echo "Running Ansible playbook..."
                    ansible-playbook -i ${INVENTORY_FILE} ${ANSIBLE_PLAYBOOK}
                '''
            }
        }
    }
}

