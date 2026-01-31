pipeline {
    agent {
        label 'tomcat'
    }

    environment {
        TOMCAT_USER = 'root'
        TOMCAT_HOST = '13.232.246.51'
        TOMCAT_WEBAPPS = '/home/ubuntu/tomcat10/webapps'
    }

    stages {
        stage('Checkout WAR') {
            steps {
                // Pull latest code/artifacts from GitHub
                git branch: 'main',
                    url: 'https://github.com/studymaterial9545-afk/nginx_install.git',
                    credentialsId: 'jenkinsAnsible'
            }
        }

        stage('Deploy WAR to Tomcat') {
            steps {
                // Use Jenkins credentials for SSH key
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkinsAnsible', keyFileVariable: 'KEYFILE')]) {
                    sh '''
                        WAR_FILE=$(ls *.war | tail -n 1)
                        echo "Deploying $WAR_FILE to Tomcat..."
                        scp -v -o StrictHostKeyChecking=no *.war root@13.232.246.51:/home/ubuntu/tomcat10/webapps/
                    '''
                }
            }
        }
    }
}








